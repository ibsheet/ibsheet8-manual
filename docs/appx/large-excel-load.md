# 대용량 엑셀 파일 처리 ***(appendix)***

<!-- synonyms: 대용량 엑셀 업로드, 대용량 엑셀 다운로드, 대용량 엑셀 로드, 엑셀 스트리밍, 스트리밍 업로드, 스트리밍 다운로드, setStreamingUploadMode, setExcelStreamingMode, directLoadExcelStreaming, directDown2Excel 스트리밍, StreamingCallback, DirectDown2ExcelCallbackInterface, pageCallback, downToBrowser, setData, setDownFinish, DirectLoadExcelUrl, 컨트롤러, 엑셀 OOME, 업로드 메모리 부족, 다운로드 메모리 부족, excel-streaming-reader, SXSSF, 행 단위 처리, 페이지 단위 처리, 페이징 다운로드, 커서 다운로드, LIMIT OFFSET, ROWNUM, setFetchSize, useCursorFetch, ResultSet 커서, 스트리밍 커서, 전량 적재, large excel upload download, streaming, 배치 insert, batch insert, 배치 업로드, 트랜잭션 롤백, insertBatch, slf4j 충돌, getLoadFinish, getDownError, setMaxFileSize -->

> 대용량 엑셀을 서버에서 업로드(로드)하거나 다운로드할 때, 전 행을 한꺼번에 메모리에 적재하면 `OOME`(OutOfMemoryError)가 발생할 수 있습니다.  
> 스트리밍 모드를 켜면 다운로드는 페이지 단위, 업로드는 행 단위로 처리해 행 수와 무관하게 서버 메모리를 일정하게 유지합니다.

> 이 문서는 데이터를 시트에 표시하지 않고 **서버에서 직접 처리**(DB 저장/조회)하는 `directDown2Excel`(다운로드)와 `directLoadExcel`(업로드) 계열을 다룹니다.  
> 서버 코드는 제품이 제공하는 `DirectDown2Excel.jsp` / `DirectLoadExcel.jsp`를 바탕으로, **콜백 안에서 DB를 직접 조회/저장**하도록 작성합니다. (구조상 서블릿 / 컨트롤러(`.do`)로 옮겨도 동작은 같습니다.)

# 다운로드 스트리밍 (directDown2Excel)

기본 방식(서버에서 전체 `List`를 만들어 `SHEETDATA`에 담아 forward)은 전 행이 메모리에 상주하므로 대용량에서 `OOME`가 날 수 있습니다.   
스트리밍 다운로드는 **페이지 단위 콜백**으로 데이터를 넘겨받아 곧바로 파일로 써 내려, 행 수와 무관하게 메모리를 일정하게 유지해 대량 데이터에서도 `OOME`를 피합니다.

> 다운로드 스트리밍은 POI에 내장된 `SXSSF`를 사용하므로 **추가 라이브러리가 필요 없습니다.** 기본 서버모듈(POI)만 설치되어 있으면 됩니다.

## 클라이언트 (JS)

`directDown2Excel`의 `url`에 다운로드를 처리할 서버 JSP를 지정하고, 조회 조건은 `extendParam`으로 보냅니다.

```javascript
sheet.directDown2Excel({
  url: "salesDown.jsp",                                  // 다운로드 처리 페이지
  extendParam: "limit=10000&fromYmd=20240101&toYmd=20241231",  // 서버로 전달할 조회 조건
  fileName: "sales.xlsx"
});
// 결과는 onExportFinish 로 받습니다 (result 1=성공 / 0=실패, message)
```

## 서버 (JSP)

제품이 제공하는 `DirectDown2Excel.jsp`를 바탕으로, 데이터를 한 번에 읽는 `setDirectRequestData()` 대신 **`setExcelStreamingMode(true)` + `eventRegistration(pageCallback)`**을 넣고, 콜백에서 페이지 단위로 DB를 조회해 반환합니다.

```jsp
<%@ page contentType="text/html;charset=UTF-8" %>
<%@ page import="java.io.*" %>
<%@ page import="java.util.*" %>
<%@ page import="com.ibleaders.ibsheet8.IBSheetDown" %>
<%@ page import="com.ibleaders.ibsheet8.util.DirectDown2ExcelCallbackInterface" %>
<%
    IBSheetDown down = null;
    try {
        out.clear();                         // JSP 출력 버퍼 비우기(바이너리 응답 준비)
        out = pageContext.pushBody();

        down = new IBSheetDown();
        down.setEncoding("UTF-8");
        down.setService(request, response);

        final int limit = Integer.parseInt(down.getExtendParam("limit"));   // 페이지 크기
        // setDirectRequestData 대신 setExcelStreamingMode + eventRegistration 추가
        down.setExcelStreamingMode(true);    // 스트리밍 켜기 (없으면 전 페이지를 메모리에 누적)
        down.eventRegistration(new DirectDown2ExcelCallbackInterface<Object>() {
            public List<Map<String, Object>> pageCallback(int pageNum) {   // 1부터 순차 호출
                try {
                    int startRow = (pageNum - 1) * limit + 1, endRow = pageNum * limit;
                    List<Map<String, Object>> rows = selectSalesPage(request, startRow, endRow);   // 페이지 조회(프로젝트 DAO/JDBC). 반환 Map key = 컬럼 Name
                    return (rows == null || rows.isEmpty()) ? null : rows;   // 더 없으면 null 로 종료
                } catch (Exception e) {
                    throw new RuntimeException(e);   // 조회 오류는 바깥 catch(getDownError)에서 표시하고 중단
                }
            }
        });

        down.downToBrowser();                // 응답에 직접 스트리밍(헤더/파일명은 모듈이 처리)
    } catch (Exception e) {
        response.setContentType("text/html;charset=utf-8");
        response.setCharacterEncoding("utf-8");
        response.setHeader("Content-Disposition", "");

        OutputStream o = response.getOutputStream();
        o.write(down.getDownError("다운로드 중 오류가 발생했습니다."));   // onExportFinish(result 0, message)
        o.flush();
    } catch (Error e) {
        response.setContentType("text/html;charset=utf-8");
        response.setCharacterEncoding("utf-8");
        response.setHeader("Content-Disposition", "");

        OutputStream o = response.getOutputStream();
        o.write(down.getDownError("다운로드 중 오류가 발생했습니다."));   // OOME 등 심각한 오류도 응답으로 알림
        o.flush();
    } finally {
        if (down != null) down.close();
    }
%>
```

콜백 안에서 **DB를 페이지 단위로 조회하는 방식**은 두 가지가 있습니다.

### 방식 A — 페이지마다 쿼리

`pageCallback`이 호출될 때마다 **그 페이지 분량(`startRow`~`endRow`)만** 조회되도록, 쿼리를 페이지 단위로 나눠 작성합니다. 매 조회가 한 페이지 크기로 한정되므로 **DB나 드라이버 설정과 무관하게 항상 메모리가 일정**해, 이식성이 높아 기본으로 권장합니다.

```sql
-- 페이지 = startRow ~ endRow 만 조회 (Oracle ROWNUM 예)
SELECT * FROM (
    SELECT a.*, ROWNUM rn FROM (
        SELECT * FROM sales WHERE pick_dt BETWEEN #{fromYmd} AND #{toYmd} ORDER BY id
    ) a WHERE ROWNUM <= #{endRow}
) WHERE rn >= #{startRow}
```

위 쿼리는 예시입니다. 페이지 범위(`startRow`~`endRow`)만 가져오면 되므로, **프로젝트의 DB와 인덱스에 맞는 가장 빠른 쿼리로 작성**하면 됩니다.

### 방식 B — 한 번만 조회하고 커서로 읽기 (ResultSet)

쿼리는 한 번만 실행하고, 열어 둔 `ResultSet` 커서에서 `pageCallback`마다 다음 청크만 읽습니다. 재조회가 없어 A의 페이지 비용이 없고, 대용량에서 더 효율적입니다.

> **주의 — 드라이버의 스트리밍 커서(전량 적재 방지)를 켜야 합니다.**  
> 많은 JDBC 드라이버는 `executeQuery()` 시점에 결과 전체를 메모리에 적재해, 커서로 나눠 읽어도 이미 전 행이 올라와 `OOME`가 납니다.  
> 드라이버가 결과를 스트리밍하도록 켜는 방법은 각 JDBC 드라이버 문서를 참고하세요.

커서(`rs`)를 콜백 밖에서 열어 두고, 콜백에서 다음 청크만 읽어 넘깁니다.

```jsp
<%@ page contentType="text/html;charset=UTF-8" %>
<%@ page import="java.io.*" %>
<%@ page import="java.util.*" %>
<%@ page import="java.sql.*" %>
<%@ page import="com.ibleaders.ibsheet8.IBSheetDown" %>
<%@ page import="com.ibleaders.ibsheet8.util.DirectDown2ExcelCallbackInterface" %>
<%
    final int PAGE_SIZE = 10000;             // 커서에서 한 번에 읽을 청크 크기
    IBSheetDown down = null;
    Connection conn = null; PreparedStatement ps = null; ResultSet rs = null;
    try {
        out.clear();                         // JSP 출력 버퍼 비우기(바이너리 응답 준비)
        out = pageContext.pushBody();

        down = new IBSheetDown();
        down.setEncoding("UTF-8");
        down.setService(request, response);

        conn = dataSource.getConnection();   // MySQL: URL 에 ?useCursorFetch=true
        ps = conn.prepareStatement(
                "SELECT * FROM sales WHERE pick_dt BETWEEN ? AND ? ORDER BY id",
                ResultSet.TYPE_FORWARD_ONLY, ResultSet.CONCUR_READ_ONLY);
        ps.setString(1, down.getExtendParam("fromYmd"));
        ps.setString(2, down.getExtendParam("toYmd"));
        ps.setFetchSize(1000);               // 스트리밍 커서(전량 적재 방지) — 켜는 법은 드라이버 문서 참고
        rs = ps.executeQuery();              // 쿼리는 한 번만 실행
        final ResultSet frs = rs;
        final ResultSetMetaData md = rs.getMetaData();
        final int cols = md.getColumnCount();

        down.setExcelStreamingMode(true);    // 스트리밍 켜기 (없으면 전 페이지를 메모리에 누적)
        down.eventRegistration(new DirectDown2ExcelCallbackInterface<Object>() {
            public List<Map<String, Object>> pageCallback(int pageNum) {   // 1부터 순차 호출
                try {
                    List<Map<String, Object>> rows = new ArrayList<Map<String, Object>>();
                    int n = 0;
                    while (n < PAGE_SIZE && frs.next()) {   // 커서에서 다음 청크만(재조회 없음)
                        Map<String, Object> row = new HashMap<String, Object>();
                        for (int i = 1; i <= cols; i++) row.put(md.getColumnLabel(i), frs.getObject(i));
                        rows.add(row); n++;
                    }
                    return rows.isEmpty() ? null : rows;   // 커서 소진이면 null 로 종료. 반환 Map key = 컬럼 Name
                } catch (SQLException e) {
                    throw new RuntimeException(e);   // 조회 오류는 바깥 catch(getDownError)에서 표시하고 중단
                }
            }
        });

        down.downToBrowser();                // 응답에 직접 스트리밍(헤더/파일명은 모듈이 처리)
    } catch (Exception e) {
        response.setContentType("text/html;charset=utf-8");
        response.setCharacterEncoding("utf-8");
        response.setHeader("Content-Disposition", "");

        OutputStream o = response.getOutputStream();
        o.write(down.getDownError("다운로드 중 오류가 발생했습니다."));   // onExportFinish(result 0, message)
        o.flush();
    } catch (Error e) {
        response.setContentType("text/html;charset=utf-8");
        response.setCharacterEncoding("utf-8");
        response.setHeader("Content-Disposition", "");

        OutputStream o = response.getOutputStream();
        o.write(down.getDownError("다운로드 중 오류가 발생했습니다."));   // OOME 등 심각한 오류도 응답으로 알림
        o.flush();
    } finally {
        if (rs != null) try { rs.close(); } catch (Exception ig) {}
        if (ps != null) try { ps.close(); } catch (Exception ig) {}
        if (conn != null) try { conn.close(); } catch (Exception ig) {}
        if (down != null) down.close();
    }
%>
```

## 다운로드 주의 사항

- **`setExcelStreamingMode(true)`가 없으면 스트리밍이 아닙니다.** 콜백만 등록하면 모듈이 전 페이지를 내부에 누적한 뒤 생성해, 행 수만큼 메모리가 증가합니다. 반드시 함께 켜세요.
- 콜백은 페이지 번호(1부터)로 순차 호출됩니다. 해당 페이지의 행 `List`를 반환하고, 더 없으면 `null`(또는 빈 리스트)을 반환해 종료합니다.
- `setExcelBuffer(int)`로 메모리에 유지할 행 수(SXSSF window)를 조정할 수 있습니다. 크게 잡으면 디스크 flush가 줄어 조금 빨라지지만 메모리를 더 씁니다.
- 서버에서 데이터만 생성해 내리는 방식이라 **데이터 행의 서식은 반영되지 않습니다** — 셀 병합, 색상, 소계/합계 등이 빠집니다.

# 업로드 스트리밍 (directLoadExcel)

`directLoadExcel()`은 업로드한 문서를 `List<Map<String, String>>` 형태로 **전 행을 한 번에 반환**합니다.  
행 수가 많으면 이 `List`가 그대로 서버 힙에 상주하므로, 대용량에서는 메모리 부족으로 처리가 실패할 수 있습니다.  
스트리밍 업로드는 행마다 콜백으로 받아 바로 처리합니다.

## 필요 라이브러리

스트리밍 업로드는 XLSX를 SAX로 읽는 `excel-streaming-reader`를 사용하므로, 서버모듈 `lib`에 아래 세 가지를 추가합니다. 버전은 현재 배포 기준(POI `5.4.1`)입니다.

- `excel-streaming-reader-5.0.4.jar`
- `poi-shared-strings-2.9.2.jar`
- `slf4j-api-1.7.36.jar`

`excel-streaming-reader`와 `poi-shared-strings`는 POI 버전에 맞춰야 하므로, 다른 POI 버전을 쓴다면 [excel-streaming-reader](https://github.com/pjfanning/excel-streaming-reader) 호환표에서 맞는 버전으로 교체하세요.

> **스프링 프로젝트 주의**: 프레임워크에 이미 `slf4j`가 포함되어 있어, 위 `slf4j-api`를 함께 넣으면 의존성 충돌이 발생합니다. 스프링에서는 `slf4j-api`를 빼고 스프링에 내장된 `slf4j`를 사용하세요.

## 설정 옵션

`IBSheetLoad`에 아래 옵션을 설정한 뒤 로드합니다.  
`setStreamingRowCacheSize`와 `setStreamingBufferSize`는 생략하면 기본값이 적용됩니다.

|메서드|기본값|설명|
|---|---|---|
|`setStreamingUploadMode(boolean)`|`false`|대용량(스트리밍) 업로드 모드 사용 여부.<br/>대용량 업로드 시 `true`로 설정합니다.|
|`setStreamingRowCacheSize(int)`|`100`|메모리에 유지할 행 수(캐시 윈도우).<br/>행을 순차로 하나씩 처리하므로 크게 잡을 이유가 거의 없어, 기본값이면 충분합니다.|
|`setStreamingBufferSize(int)`|`4096`|업로드 파일을 읽어들일 때의 버퍼 크기(byte).<br/>대부분 기본값이면 충분합니다.|

## 행 단위 콜백 (directLoadExcelStreaming)

`directLoadExcelStreaming(StreamingCallback)`은 전 행을 `List`로 반환하지 않고 **행마다 콜백을 호출**합니다.  
콜백에서 받은 한 행을 즉시 처리(DB insert 등)하면 그 행은 메모리에 남지 않으므로, 로드한 데이터를 한꺼번에 메모리에 올리지 않아 메모리 사용량을 크게 줄일 수 있습니다.

|파라미터|타입|필수|설명|
|---|---|---|---|
|callback|`StreamingCallback`|필수|행마다 호출되는 콜백.<br/>`callback(Map<String, String> map)`의 `map`은 데이터 한 행이며, key는 시트 컬럼 `Name`입니다.|
|sheetIdx|`int`|선택|여러 워크시트 중 로드할 시트 인덱스.<br/>`directLoadExcelStreaming(int sheetIdx, StreamingCallback)` 형태로 지정합니다.|

## 클라이언트 (JS)

`Cfg.Export.DirectLoadExcelUrl`에 업로드를 처리할 JSP를 지정하고 `directLoadExcel()`을 호출합니다. (`DirectLoadExcelUrl`을 지정하면 `Url` 규칙 대신 이 경로로 파일이 전송됩니다.)

```javascript
IBSheet.create({
  id: "sheet",
  el: "sheetDiv",
  options: {
    Cfg: {
      Export: { DirectLoadExcelUrl: "salesUpload.jsp" }   // 업로드 처리 페이지
    },
    Events: {
      // 서버의 getLoadFinish/getLoadError 결과를 여기서 받음
      onImportFinish: function (evtParam) {
        if (evtParam.result < 0) alert("업로드 실패: " + evtParam.message);
        else alert("업로드가 완료되었습니다.");
      }
    },
    Cols: [ /* 컬럼 정의 */ ]
  }
});

// 버튼을 클릭하면 파일 선택창이 뜨고, 고른 파일이 DirectLoadExcelUrl 로 전송됩니다
document.getElementById("directLoadExcel").addEventListener("click", function () {
  sheet.directLoadExcel();
});
```

## 서버 (JSP)

제품이 제공하는 `DirectLoadExcel.jsp`를 바탕으로, `directLoadExcel()`(List 반환) 자리에 **`setStreamingUploadMode(true)` + `directLoadExcelStreaming(callback)`**을 넣고, 콜백에서 한 행씩 바로 저장합니다.

콜백은 데이터 행을 하나씩 받습니다. `map`은 한 행이고 key는 시트 컬럼 `Name`입니다. 받은 행을 그 자리에서 처리(insert)하면 됩니다.

```jsp
<%@ page contentType="text/html;charset=UTF-8" %>
<%@ page import="java.io.*" %>
<%@ page import="java.util.*" %>
<%@ page import="com.ibleaders.ibsheet8Loader.IBSheetLoad" %>
<%@ page import="com.ibleaders.ibsheet8Loader.StreamingCallback" %>
<%@ page import="com.ibleaders.ibsheet8.exception.IBSheetException" %>
<%@ page import="com.ibleaders.ibsheet8.exception.StreamingCallbackException" %>
<%
    out.clear();
    out = pageContext.pushBody();

    IBSheetLoad load = null;
    final int[] cnt = { 0 };   // 처리한 행 수
    try {
        load = new IBSheetLoad();
        load.setStreamingUploadMode(true);   // 스트리밍 업로드 모드
        load.setEncoding("UTF-8");
        load.setService(request, response);  // 업로드 파일(멀티파트) 수신

        load.directLoadExcelStreaming(new StreamingCallback() {
            public void callback(Map<String, String> map) throws StreamingCallbackException {
                try {
                    cnt[0]++;
                    salesDao.insert(map);              // 데이터 한 행 저장 (map key = 시트 컬럼 Name)
                } catch (Exception e) {
                    // 중단하려면 StreamingCallbackException 을 던진다(메시지는 onImportFinish 로 전달).
                    throw new StreamingCallbackException("행 처리 중 오류가 발생했습니다.", e);
                }
            }
        });

        // 완료 신호를 보내야 onImportFinish(성공)가 발생하고 대기 이미지가 풀립니다.
        OutputStream out2 = response.getOutputStream();
        out2.write(load.getLoadFinish("EXCEL", 1, cnt[0] + "건 업로드 완료"));
        out2.flush();
    } catch (IBSheetException e) {
        OutputStream err = response.getOutputStream();
        err.write(load.getLoadError(e.getErrorCode(), e.getErrorMessage()));
        err.flush();
    } catch (Exception e) {
        OutputStream err = response.getOutputStream();
        err.write(load.getLoadError());   // 그 외 오류는 기본 메시지로 응답
        err.flush();
    } catch (Error e) {
        OutputStream err = response.getOutputStream();
        err.write(load.getLoadError());   // OOME 등 심각한 오류도 응답으로 알림
        err.flush();
    } finally {
        if (load != null) load.close();
    }
%>
```

일반 방식에서 `setService` 뒤에 호출하던 `directLoadExcel()`(List 반환)이나 `sendDirectToFP()`(FP 페이지로 forward)를, 대용량에서는 이 `directLoadExcelStreaming(callback)`이 대신합니다.

### 성능 — 묶음 insert

한 행씩 insert하면 DB 왕복이 많아 대용량에서 느립니다. **일정 개수씩 모아 한 번에 실행(묶음 insert)한 뒤 비우고, 스트림이 끝난 뒤 남은 자투리를 flush**하면 빠르면서도 그 한 묶음만 메모리에 있어 스트리밍이 유지됩니다.  
아래 예제는 **오류 시 전체 롤백**을 위해 업로드를 한 트랜잭션으로 묶습니다(중간에 실패하면 이미 넣은 묶음까지 되돌립니다).  
단, 수백만 행을 한 트랜잭션으로 열면 트랜잭션 로그가 커질 수 있어, 그럴 땐 묶음마다 커밋하고, 실패 시 정리하는 전략을 씁니다.

아래는 위 업로드 예제에 **묶음 insert와 트랜잭션을 적용한 전체 예제**입니다. 앞 예제와 비교하면, 콜백 안 `insert(map)`이 묶음 insert로 바뀌고 커넥션을 한 트랜잭션으로 묶어(`setAutoCommit(false)` → `commit`/`rollback`) 중간 실패 시 넣은 묶음까지 되돌리는 점만 다릅니다. 트랜잭션 `try`는 `load` 수명의 바깥 `try` 안에 중첩되고, 롤백 시 `throw`가 바깥 `catch`로 전달돼 `getLoadError`가 호출됩니다.

```jsp
<%@ page contentType="text/html;charset=UTF-8" %>
<%@ page import="java.io.*" %>
<%@ page import="java.util.*" %>
<%@ page import="java.sql.*" %>
<%@ page import="com.ibleaders.ibsheet8Loader.IBSheetLoad" %>
<%@ page import="com.ibleaders.ibsheet8Loader.StreamingCallback" %>
<%@ page import="com.ibleaders.ibsheet8.exception.IBSheetException" %>
<%@ page import="com.ibleaders.ibsheet8.exception.StreamingCallbackException" %>
<%
    out.clear();
    out = pageContext.pushBody();

    IBSheetLoad load = null;
    Connection conn = null;
    final int BATCH = 1000;   // 한 번에 모아 insert할 행 묶음 크기
    final List<Map<String, String>> buffer = new ArrayList<Map<String, String>>();
    final int[] cnt = { 0 };   // 처리한 행 수
    try {
        load = new IBSheetLoad();
        load.setStreamingUploadMode(true);   // 스트리밍 업로드 모드
        load.setEncoding("UTF-8");
        load.setService(request, response);

        conn = dataSource.getConnection();
        conn.setAutoCommit(false);           // 업로드 전체를 한 트랜잭션으로 (오류 시 전체 롤백)
        final Connection fconn = conn;

        try {   // 트랜잭션 try (load 수명의 바깥 try 안에 중첩)
            load.directLoadExcelStreaming(new StreamingCallback() {
                public void callback(Map<String, String> map) throws StreamingCallbackException {
                    try {
                        cnt[0]++;
                        buffer.add(map);
                        if (buffer.size() >= BATCH) {   // 모아둔 행이 BATCH(1000)만큼 차면 한 번에 insert 후 비움
                            salesDao.insertBatch(fconn, buffer);   // 모아둔 한 묶음을 INSERT — addBatch로 쌓고 executeBatch로 한 번에 전송
                            buffer.clear();
                        }
                    } catch (Exception e) {
                        throw new StreamingCallbackException("행 처리 중 오류가 발생했습니다.", e);
                    }
                }
            });
            if (!buffer.isEmpty()) { salesDao.insertBatch(fconn, buffer); buffer.clear(); }   // 남은 자투리 flush
            conn.commit();     // 전부 성공하면 커밋
        } catch (Exception e) {
            conn.rollback();   // 중간에 오류나면 넣은 묶음까지 롤백
            throw e;           // 바깥 catch 로 넘겨 getLoadError 처리
        }

        // 완료 신호를 보내야 onImportFinish(성공)가 발생하고 대기 이미지가 풀립니다.
        OutputStream out2 = response.getOutputStream();
        out2.write(load.getLoadFinish("EXCEL", 1, cnt[0] + "건 업로드 완료"));
        out2.flush();
    } catch (IBSheetException e) {
        OutputStream err = response.getOutputStream();
        err.write(load.getLoadError(e.getErrorCode(), e.getErrorMessage()));
        err.flush();
    } catch (Exception e) {
        OutputStream err = response.getOutputStream();
        err.write(load.getLoadError());   // 그 외 오류는 기본 메시지로 응답
        err.flush();
    } catch (Error e) {
        OutputStream err = response.getOutputStream();
        err.write(load.getLoadError());   // OOME 등 심각한 오류도 응답으로 알림
        err.flush();
    } finally {
        if (conn != null) try { conn.close(); } catch (Exception ig) {}
        if (load != null) load.close();
    }
%>
```

## 업로드 주의 사항

- 콜백 처리 중 오류가 나면 업로드를 멈추고 싶을 수 있습니다. 이때 위 예제처럼 `StreamingCallbackException`을 던지면 스트리밍이 중단되고 메시지가 `onImportFinish`로 전달됩니다.
- `XLSX`는 `excel-streaming-reader`(SAX) 방식으로 읽어 메모리가 일정하게 유지됩니다. `XLS`(구형 이진 형식)는 전체 로드 방식이라 스트리밍 이점이 제한적입니다.
- 업로드 파일 크기 자체를 제한하려면 `setMaxFileSize`를 함께 사용합니다.

## Read More
- [directDown2Excel method](/docs/funcs/excel/direct-down-to-excel)
- [directLoadExcel method](/docs/funcs/excel/direct-load-excel)
- [Export cfg](/docs/props/cfg/export)
- [엑셀파일 업로드/다운로드 appendix](/docs/appx/import-export)
- [서버모듈 함수 appendix](/docs/appx/server-module-functions)

## Since

|product|version|desc|
|---|---|---|
|jar|2.1.6|스트리밍 다운로드(`directDown2Excel` + `setExcelStreamingMode`) 추가|
|jar|1.1.41|스트리밍 업로드(`directLoadExcelStreaming`) 추가|
