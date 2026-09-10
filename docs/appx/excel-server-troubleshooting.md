# 엑셀 서버 모듈 트러블슈팅 ***(appendix)***

<!-- synonyms: 엑셀 다운로드 안됨, 엑셀 업로드 안됨, XssFilter 엑셀, HtmlFilter 엑셀, MarkupTagDelimiter, csrf 엑셀, X-Frame-Options 엑셀, Spring Security 엑셀, jsp 없이 엑셀, 서블릿 엑셀, 엑셀 필터 인코딩, iframe 엑셀 차단, getDownError, getLoadError, directDown2Excel 오류 메시지, directLoadExcel 오류 처리, 중계 페이지 오류 메시지, 조회 건수 초과 안내, 다운로드 막기, onExportFinish 오류, onImportFinish 오류, CORS 엑셀, 크로스 도메인 엑셀, Access-Control 엑셀, useXhr CORS, 멀티파트 리졸버, MultipartFile, setService NullPointerException, 본문 선소비, setData, columnTag, jsp 서블릿 변환, 컨트롤러 엑셀 -->

> 서버 모듈([down2Excel](/docs/funcs/excel/down-to-excel) / [loadExcel](/docs/funcs/excel/load-excel)) 사용 시 자주 겪는 환경 문제와 해결 방법입니다.

## jsp 대신 서블릿(컨트롤러)로 처리

> **JSP를 쓸 수 없는 환경**에서는 서버 모듈 처리를 서블릿(컨트롤러)으로 작성합니다.

엑셀 업로드/다운로드는 **멀티파트 요청**을 서버에 보냅니다.  
이 요청을 보안, XSS, 인코딩 같은 필터나 스프링 멀티파트 리졸버가 먼저 읽어버리면, `setService`가 본문을 다시 못 읽어 `NullPointerException`이 납니다.  
이때는 `request.getParameter("Data")`나 `MultipartFile`로 받아 `setData`로 넘기면 해결됩니다.  
특히 멀티파트 리졸버가 본문을 이미 파싱한 환경에서는 업로드 파일을 컨트롤러의 `MultipartFile`로 받아야 하므로, 이런 경우에도 jsp 대신 컨트롤러에서 처리합니다.
- **다운로드**: 화면이 보낸 시트 정보와 데이터를 `setData(request.getParameter("Data"))`로 받습니다.
- **업로드**: 시트 정보와 함께 엑셀 파일이 오므로 `MultipartFile`로 파일을 받아 임시 파일로 저장한 뒤 `setData(request.getParameter("columnTag"), 임시파일경로)`로 넘깁니다.

jsp를 사용할 수 없거나 서블릿(컨트롤러) 방식을 택했다면, 제공되는 jsp(`Down2Excel.jsp`, `LoadExcel.jsp` 등)의 로직을 Java 코드로 옮겨 직접 구현합니다.
- Spring MVC: `@Controller` / `@RestController`에서 처리
- 서블릿: `HttpServlet`의 `doGet()` / `doPost()`에서 처리

서블릿 API 패키지는 환경에 따라 다릅니다. (Java EE는 `javax.servlet`, Jakarta EE는 `jakarta.servlet`)

```java
// 예: down2Excel — Down2Excel.jsp 로직을 컨트롤러로 옮긴 형태
@RequestMapping(value = "/excel/down2Excel.do", method = RequestMethod.POST)
public void down2Excel(HttpServletRequest req, HttpServletResponse res) throws Exception {
    res.setContentType("application/octet-stream");
    res.setCharacterEncoding("UTF-8");
    IBSheetDown down = null;
    try {                                       // Down2Excel.jsp 의 try 내용
        down = new IBSheetDown();
        down.setEncoding("UTF-8");
        down.setData(req.getParameter("Data"));   // 시트 정보(컬럼) + 데이터
        down.setService(req, res);
        down.setFileType("excel");
        down.downToBrowser();
    } catch (Exception e) {                     // Down2Excel.jsp 의 catch 내용
        res.setContentType("text/html;charset=utf-8");
        OutputStream o = res.getOutputStream();
        o.write(down.getDownError("다운로드 중 오류가 발생했습니다."));
        o.flush();
    } finally {
        if (down != null) down.close();
    }
}
```

각 함수의 환경 설정 옵션 전체와 `down2Pdf` / `down2Text` / `loadText`까지 포함한 **전체 컨트롤러 복붙 예제**는 [엑셀 서버모듈 컨트롤러 전체 예제](/docs/appx/excel-servlet-controller-sample)를 참고하세요.

## Html Filter / Xss Filter 적용 후 다운로드와 업로드가 안 되는 경우

엑셀 다운로드/업로드 시 시트 정보(컬럼 정의 등)와 데이터가 XML 형식으로 서버에 전송됩니다.   
보안 필터가 적용되면 `<`, `>`, `(`, `)` 등의 문자가 `&lt;`, `&gt;` 등으로 인코딩되어 엑셀 로직이 정상 동작하지 않습니다.

해결하려면 특수문자 대신 사용할 구분자를 클라이언트와 서버 양쪽에 동일하게 지정합니다.
- 클라이언트: `Cfg`의 `MarkupTagDelimiter` 설정
- 서버: 엑셀 처리 모듈(jsp/servlet)에서 `setMarkupTagDelimiter` 설정

두 설정 값은 반드시 같아야 하며, 이렇게 하면 필터가 건드리지 않는 구분자를 사용하므로 정상 처리됩니다.

## Spring Security CSRF 토큰 / X-Frame-Options 문제

Spring Security 사용 시 `Refused to display in a frame because it set 'X-Frame-Options' to 'deny'` 오류로 다운로드/업로드가 차단될 수 있습니다.  
IBSheet은 기본적으로 iframe 기반 폼 제출(Form submit) 방식을 사용하기 때문입니다.

해결하려면 요청을 XHR 방식으로 전환합니다.
- `reqHeader`를 지정하면 iframe 폼 제출에서 XHR 방식으로 자동 전환되어, 요청 헤더에 CSRF 토큰이나 인증 정보를 직접 담을 수 있습니다.
- 또는 `useXhr` 옵션으로 XHR 전송을 명시적으로 강제합니다.

```javascript
sheet.down2Excel({
    reqHeader: { "X-CSRF-TOKEN": "토큰값" }   // reqHeader 지정 시 XHR로 전환, 헤더에 CSRF 토큰 포함
});

sheet.loadExcel({
    reqHeader: { "X-CSRF-TOKEN": "토큰값" }
});
```

## XHR 전송(`useXhr` / `reqHeader`) 시 크로스 도메인(CORS)

위 CSRF 처리처럼 `reqHeader`나 `useXhr`을 쓰면 전송이 **XHR(ajax)** 로 바뀝니다.  
기본 iframe form submit은 CORS 제약을 받지 않지만, **XHR은 크로스 도메인일 때 CORS가 적용**되어, 다른 도메인 서버로 보내면 CORS 허용 헤더가 없을 때 오류가 납니다.

- XHR이 꼭 필요치 않으면 **기본 form submit**(`useXhr` 미설정)으로 두어 CORS를 피합니다.
- XHR을 써야 하면 서버에서 `Access-Control-Allow-Origin` 등 CORS 허용 헤더를 설정합니다.
- 커스텀 헤더(`X-CSRF-TOKEN`)를 쓰면 `Access-Control-Allow-Headers`도 필요합니다.

**다운로드에서 CORS 헤더를 직접 넣을 때 주의**: `down.downToBrowser()`는 내부적으로 `response.reset()`을 호출해 앞서 설정한 헤더를 지웁니다. 이땐 `downToBrowser()`를 풀어 써 그 사이에서 헤더를 설정합니다.

```java
// down.downToBrowser(); 대신
down.setFileHeader();
response.setHeader("Access-Control-Allow-Origin", request.getHeader("Origin"));
down.downToStream(response.getOutputStream());
```

같은 도메인이면 위 설정은 모두 불필요합니다.

## directDown2Excel 중계 페이지에서 오류 메시지 보내기 (getDownError)

`directDown2Excel`을 호출하면 요청이 `url`로 지정한 **페이지**로 전달됩니다.  
서버 오류나 조회 건수 초과 같은 조건에서 다운로드를 막고 안내 메시지를 띄우려면, 엑셀 파일 대신 `getDownError`(`IBSheetDown`의 메소드)로 **오류 응답**을 내려보냅니다.   
이 메시지는 클라이언트 [onExportFinish](/docs/events/on-export-finish) 이벤트의 `message`로 전달됩니다.

```java
List<Map<String, Object>> list = queryData(...);

if (list.size() > 100000) {                  // 오류 조건 (예: 건수 초과)
    IBSheetDown down = new IBSheetDown();
    down.setService(request, response);
    OutputStream out2 = response.getOutputStream();
    out2.write(down.getDownError("조회 건수가 너무 많습니다.<br/>기간을 나누어 조회해 주십시오."));
    out2.flush();
} else {                                      // 정상: SHEETDATA 설정 후 forward (DirectDown2Excel.jsp가 downToBrowser)
    request.setAttribute("SHEETDATA", list);
    request.getRequestDispatcher("./DirectDown2Excel.jsp").forward(request, response);
}
```

- `getDownError()`(인자 없음) : 기본 오류 메시지 전송
- `getDownError("메시지")` : 지정한 메시지 전송 (HTML `<br/>` 사용 가능)

클라이언트에서는 [onExportFinish](/docs/events/on-export-finish)의 `result`로 성공(`1`)/실패(`0`)를 판정하고, 실패 시 `message`로 사용자에게 안내합니다.

```javascript
options.Events = {
    onExportFinish: function (evtParam) {
        if (!evtParam.result) {        // 0 = 실패
            alert(evtParam.message);   // 서버가 보낸 오류 메시지
        }
    }
};
```

## directLoadExcel 처리 중 오류 메시지 보내기 (getLoadError)

`directLoadExcel` 함수를 호출하면 선택한 엑셀 파일이 `DirectLoadExcel.jsp`(또는 이를 옮긴 컨트롤러)로 전달됩니다.  
`DirectLoadExcel.jsp`가 엑셀을 **읽어(파싱)** 데이터를 만든 뒤, `extendParam`의 `FP`로 지정한 페이지로 데이터를 forward하고, 그 페이지에서 DB 저장 등을 처리합니다.   
**FP 페이지에서 개발자가 다루는 오류는 저장 단계**(검증 실패, DB 저장 실패 등)입니다.

`getLoadError(코드, 메시지)`(실패)와 `getLoadFinish(type, 코드, 메시지)`(성공)가 넘긴 값은 클라이언트 [onImportFinish](/docs/events/on-import-finish)의 `result`(코드)와 `message`로 전달됩니다.  
에러인지 정상인지는 **넘긴 `result` 코드의 부호로 정해집니다**(음수면 에러, 0 이상이면 정상). 그래서 커스텀 오류는 `-500`처럼 음수 코드로([onImportFinish](/docs/events/on-import-finish)에 정의된 내부 코드와 겹치지 않게) 보냅니다.  
성공 시 `getLoadFinish`로 완료 신호를 보내지 않으면 클라이언트가 완료를 인지하지 못할 수 있습니다.

```java
// 개발자가 작성한 FP 페이지 — DirectLoadExcel.jsp가 파싱해 forward한 데이터를 받아 저장
IBSheetLoad load = new IBSheetLoad();
load.setEncoding("UTF-8");
load.setService(request, response);   // getLoadError가 response를 사용하므로 필수 (없으면 NPE)

try {
    // 전달받은 데이터를 검증하고 저장 (개발자 로직)
    // saveToDatabase(...);

    // 성공: 완료 신호를 보냄 (result 0 이상 = 정상 → onImportFinish)
    OutputStream out2 = response.getOutputStream();
    out2.write(load.getLoadFinish("EXCEL", 1, "업로드 완료"));
    out2.flush();
} catch (Exception e) {
    OutputStream out2 = response.getOutputStream();
    // 저장/검증 실패 시 코드와 메시지를 지정해 전달 (음수 코드 = 에러)
    out2.write(load.getLoadError(-500, "저장 중 오류가 발생했습니다. 입력값을 확인해 주세요."));
    out2.flush();
    return;
}
```

**메시지에 따옴표, 역슬래시, 줄바꿈을 그대로 넣지 마세요.**   
`getLoadError`와 `getLoadFinish`가 넘긴 메시지는 응답 스크립트(`postMessage('...^{"message":"..."}', '*')`)에 **이스케이프 없이 그대로** 실립니다.   
이 응답은 메시지를 두 겹으로 감싸는데, 바깥은 작은따옴표로 감싼 JS 문자열이고 안쪽은 큰따옴표로 감싼 JSON입니다.   
그래서 메시지에 큰따옴표(`"`)가 있으면 JSON이 깨지고, 작은따옴표(`'`)가 있으면 JS 문자열이 깨져서 스크립트가 실행되지 않고 [onImportFinish](/docs/events/on-import-finish)가 **발생하지 않습니다**(에러도 성공도 아무 반응이 없음).   
예외 메시지(`e.getMessage()`)에는 따옴표가 자주 포함되므로(`For input string: "..."` 등), 사용자에게 보낼 메시지는 이런 문자를 제거하거나 치환한 뒤 전달합니다.

```java
// 예외 메시지를 그대로 넘기지 말고, 따옴표와 역슬래시, 줄바꿈을 제거한 뒤 전달
String safeMsg = (rowNo + "행 처리 오류: " + e.getMessage())
        .replace("\\", "")
        .replace("\"", "")
        .replace("'", "")
        .replaceAll("[\r\n]", " ");
out2.write(load.getLoadError(-500, safeMsg));
```

**여러 행을 반복 저장하다가 중간에 오류가 나는 경우**는, 전체를 한 트랜잭션으로 묶고 오류 시 `rollback`한 뒤 `getLoadError`로 알립니다.    
`getLoadError`는 오류 응답을 만들 뿐 반복문을 멈추지 않으므로, 반드시 `return`(또는 `break`)으로 흐름을 함께 끊어야 합니다(그러지 않으면 다음 행에서 다시 응답을 써서 응답이 겹칩니다).

```java
// 전달받은 데이터를 반복 저장 — 한 건이라도 실패하면 전체 롤백 후 중단
List<Map<String, Object>> rows = (List<Map<String, Object>>) request.getAttribute("SHEETDATA");

IBSheetLoad load = new IBSheetLoad();
load.setEncoding("UTF-8");
load.setService(request, response);   // getLoadError/getLoadFinish가 response를 사용 → 필수

Connection conn = null;
int rowNo = 0;
try {
    conn = getConnection();
    conn.setAutoCommit(false);        // 전체를 한 트랜잭션으로 묶음

    for (Map<String, Object> row : rows) {
        rowNo++;
        saveRow(conn, row);           // 저장 중 오류(SQLException 등) 발생 가능
    }

    conn.commit();                    // 전부 성공
    OutputStream out2 = response.getOutputStream();
    out2.write(load.getLoadFinish("EXCEL", 1, rows.size() + "건 저장 완료"));
    out2.flush();
} catch (Exception e) {               // 처리 중 오류
    if (conn != null) conn.rollback();   // 이미 저장한 행까지 전체 취소
    OutputStream out2 = response.getOutputStream();
    out2.write(load.getLoadError(-500, rowNo + "행 처리 중 오류로 저장을 취소했습니다."));
    out2.flush();
    return;                           // 응답을 썼으면 반드시 흐름 중단
} finally {
    if (conn != null) conn.close();
}
```

클라이언트에서는 [onImportFinish](/docs/events/on-import-finish)의 `result`(코드)로 성공/실패를 판정하고, 실패 시 `message`로 사용자에게 안내합니다.

```javascript
options.Events = {
    onImportFinish: function (evtParam) {
        if (evtParam.result < 0) {     // 음수 = 에러
            alert(evtParam.message);   // 서버가 보낸 오류 메시지
        }
    }
};
```

### Read More
- [엑셀파일 업로드/다운로드 appendix](/docs/appx/import-export)
- [down2Excel method](/docs/funcs/excel/down-to-excel)
- [loadExcel method](/docs/funcs/excel/load-excel)
