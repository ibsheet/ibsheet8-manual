# 서버모듈 함수  ***(appendix)***

<!-- synonyms: 서버모듈 함수, 서버모듈 API, 서버 API, jsp API, 서버 사이드, IBSheetDown, IBSheetLoad, Print2Pdf, 엑셀 서버 다운로드, 엑셀 서버 업로드, 엑셀 서버 함수, PDF 서버, setEncoding, setFontName, setFileType, setMaxRows, setFontFolder, setData, setLog, getDownError, getLoadError, setDisallowDuplicatedHeader, loadFile, 서버모듈 버전 확인, getVersion, 서버 에러 처리, 중복 헤더, server module api, server function -->

> 서버모듈(jsp)에서 사용하는 **Java API**입니다.  
> 엑셀/텍스트 **다운로드**는 `IBSheetDown`, **업로드**는 `IBSheetLoad`, **PDF 다운로드**는 `Print2Pdf` 클래스를 사용합니다.  
> 서버모듈 설치와 jsp 설정은 [엑셀파일 업로드/다운로드](/docs/appx/import-export)를 참고하세요.

## API 사용

서버모듈 API를 사용하려면 먼저 생성자를 호출해 객체를 만들어야 합니다.

```java
// request, response를 포함해 IBSheetDown 생성자 호출
IBSheetDown down = new IBSheetDown(request, response);

// 인코딩 설정
down.setEncoding("UTF-8");

// 다운로드 파일명 반환
down.getFileName();
```

## IBSheetDown (다운로드)

`XLSX`, `XLS`, `CSV`, `TEXT` 파일을 다운로드합니다.

### 생성자
|생성자|설명|
|---|---|
|`IBSheetDown()`|request/response 할당이 없으므로 `setService`로 등록해야 정상 동작합니다.|
|`IBSheetDown(HttpServletRequest, HttpServletResponse)`|request와 response를 포함한 생성자|
|`IBSheetDown(HttpServletRequest, HttpServletResponse, int)`|`DelimMode 1`을 사용할 때의 생성자. 시트 문자열에 `STX(\u0002)`, `ETX(\u0003)`가 포함된 경우에만 `1`로 설정합니다.|

### appendDataArr(data)
시트에 `String[]` 형태의 데이터를 한 줄 덧붙입니다. (`DirectDown2Excel` 전용)

|파라미터|타입|필수|설명|
|---|---|---|---|
|data|`String[]`|필수|엑셀에 추가할 시트 데이터|

### appendDataList(data)
시트에 `List` 형태의 데이터를 한 줄 덧붙입니다. (`DirectDown2Excel` 전용)

|파라미터|타입|필수|설명|
|---|---|---|---|
|data|`List<String>`|필수|엑셀에 추가할 시트 데이터|

### appendDataMap(data)
시트에 `Map` 형태의 데이터를 한 줄 덧붙입니다. (`DirectDown2Excel` 전용)

|파라미터|타입|필수|설명|
|---|---|---|---|
|data|`Map<String, String>`|필수|엑셀에 추가할 시트 데이터|

### appendMultiData(data)
시트에 데이터를 여러 줄 덧붙입니다. (`DirectDown2Excel` 전용)

|파라미터|타입|필수|설명|
|---|---|---|---|
|data|`List<Object>`|필수|엑셀에 추가할 시트 데이터|

### close()
다운로드를 종료하고 메모리를 해제합니다.

### downToBrowser()
생성된 문서를 브라우저를 통해 다운로드합니다.

### downToStream(OutputStream)
생성된 문서를 `OutputStream`으로 전송합니다.

### getDownError(errorCode, message)
다운로드 중계 페이지(주로 `directDown2Excel`)에서 조건 불충족 등으로 파일 대신 에러를 내려보낼 때 사용합니다. `downToBrowser()` 대신 반환된 `byte[]`를 `OutputStream`으로 출력하면, 클라이언트 `onExportFinish` 이벤트에 실패(`result` `0`)로 전달되어 `message`로 안내할 수 있습니다. 인자 없이 `getDownError()`를 호출하면 기본 에러 메시지가, `getDownError(message)`는 메시지만 지정하는 형태입니다.

|파라미터|타입|필수|설명|
|---|---|---|---|
|errorCode|`int`|선택|에러 코드|
|message|`String`|선택|사용자에게 표시할 커스텀 메시지 (HTML `<br/>` 사용 가능)|

```java
// 정상은 downToBrowser(), 에러 조건에서만 getDownError 출력
OutputStream out = response.getOutputStream();
out.write(down.getDownError("조회 건수가 너무 많습니다."));
out.flush();
```

### getExtendParam(key)
시트에서 전달한 `ExtendParam` 정보를 받습니다. (반환: `String`, key에 해당하는 값)

|파라미터|타입|필수|설명|
|---|---|---|---|
|key|`String`|필수|`ExtendParam`에 설정한 Key 값|

### getFileName()
생성된 파일명을 반환합니다. (반환: `String`)

### saveToFile(path)
생성된 문서를 서버의 특정 폴더에 저장합니다.

|파라미터|타입|필수|설명|
|---|---|---|---|
|path|`String`|필수|저장할 서버 폴더 명|

### setData(data)
클라이언트가 보낸 시트 전문(`Data` 파라미터)을 세팅합니다.  
멀티파트 필터가 걸린 환경이나 `multipart: 0`(일반 POST) 전송 시, 서버에서 `request.getParameter("Data")`로 읽어 `setService` 호출 **전에** 세팅해야 합니다.

|파라미터|타입|필수|설명|
|---|---|---|---|
|data|`String`|선택|클라이언트가 전송한 시트 전문(`Data`)|

```java
String data = request.getParameter("Data");
down.setData(data);   // setService 호출 전에 먼저 세팅
```

### setDirectRequestData()
`HttpRequest`에 `SHEETDATA`라는 Attribute가 저장되어 있는 경우, 해당 데이터를 다운로드합니다. (`DirectDown2Excel` 전용)

### setDownFinish()
다운로드 종료 정보를 시트에 전달하고, 화면의 대기 이미지를 닫기 위한 `FileDownloadToken` 쿠키를 생성합니다.

### setLog(isLog)
서버 콘솔에 다운로드 처리 상세 로그를 출력할지 설정합니다. 브라우저나 서버 콘솔에 별다른 에러 없이 다운로드가 실패할 때 원인 파악에 사용합니다.   
출력 로그에는 처리 시점의 JVM 메모리, 파일 정보, 소요 시간 등이 포함되며, `excel mode=POI`가 표시되면 POI 라이브러리가 정상 로드되어 동작 중인 것입니다.

|파라미터|타입|필수|설명|
|---|---|---|---|
|isLog|`boolean`|필수|상세 로그 출력 여부|

### setEncoding(encoding)
파일을 다운로드받는 HTML 페이지의 인코딩에 맞춰 인코딩을 설정합니다.

|파라미터|타입|필수|설명|
|---|---|---|---|
|encoding|`String`|필수|페이지 인코딩 타입 (`UTF-8`, `EUC-KR` 등)|

### setFileHeader()
다운로드할 파일의 정보를 브라우저 헤더로 전송합니다.

### setFontName(fontName)
문서에 사용될 글꼴을 설정합니다. (HeaderFontName도 함께 설정됩니다.)

|파라미터|타입|필수|설명|
|---|---|---|---|
|fontName|`String`|필수|엑셀 파일에 설정할 글꼴|

### setFontSize(size)
문서에 사용될 글자 크기를 설정합니다. (HeaderFontSize도 함께 설정됩니다.)

|파라미터|타입|필수|설명|
|---|---|---|---|
|size|`int`|필수|엑셀 파일에 설정할 글자 크기|

### setHeaderBackColor(color)
헤더 부분의 배경색을 설정합니다.

|파라미터|타입|필수|설명|
|---|---|---|---|
|color|`String`|필수|엑셀 파일의 헤더 배경색|

### setHeaderFontBold(bold)
헤더 부분 글자의 볼드 처리 여부를 설정합니다.

|파라미터|타입|필수|설명|
|---|---|---|---|
|bold|`boolean`|필수|헤더 글자 볼드 처리 여부 (default: `false`)|

### setHeaderFontColor(color)
헤더 부분의 글자색을 설정합니다.

|파라미터|타입|필수|설명|
|---|---|---|---|
|color|`String`|필수|엑셀 파일의 헤더 글자 색상|

### setHeaderFontName(name)
헤더 부분에 사용될 글꼴을 설정합니다.

|파라미터|타입|필수|설명|
|---|---|---|---|
|name|`String`|필수|엑셀 파일의 헤더 글꼴|

### setHeaderFontSize(fontSize)
헤더 부분에 사용될 글자 크기를 설정합니다.

|파라미터|타입|필수|설명|
|---|---|---|---|
|fontSize|`int`|필수|엑셀 파일의 헤더 글자 크기|

### setWordWrap(isWordWrap)
문서에 줄바꿈 적용 여부를 설정합니다.

|파라미터|타입|필수|설명|
|---|---|---|---|
|isWordWrap|`boolean`|필수|엑셀 파일의 줄바꿈 허용 여부|

### setMarkupTagDeilmiter(startTag1, startTag2, closingTag1, closingTag2)
기본 마크업 태그 외에 별도의 태그를 사용할 때 설정합니다. IBSheet8 환경설정(`ibsheet.cfg`)의 `MarkupTagDelimiter` 설정 값과 동일해야 합니다.

|파라미터|타입|필수|설명|
|---|---|---|---|
|startTag1|`String`|필수|Start Tag 시작 문자열 (default: `<`)|
|startTag2|`String`|필수|Start Tag 완료 문자열 (default: `>`)|
|closingTag1|`String`|필수|Closing Tag 시작 문자열 (default: `</`)|
|closingTag2|`String`|필수|Closing Tag 완료 문자열 (default: `>`)|

### setDelimMode(mode)
시트 문자열에 `STX(\u0002)`, `ETX(\u0003)`가 포함된 경우 설정합니다.

|파라미터|타입|필수|설명|
|---|---|---|---|
|mode|`boolean`|필수|`0`: 시트 구분자로 STX, ETX 문자를 사용 (default)<br/>`1`: 시트 구분자로 변형된 문자열을 사용 (시트에 설정되어 있어야 함)|

### setFileType(fileType, ignoreFileExtention)
다운로드할 문서의 타입을 설정합니다.

|파라미터|타입|필수|설명|
|---|---|---|---|
|fileType|`String`|필수|`xls`: xls 형식<br/>`xlsx`: xlsx 형식<br/>`excel`: FileName에 설정한 값으로 다운로드(확장자 없으면 기본 xls)|
|ignoreFileExtention|`boolean`|선택|클라이언트에서 설정한 파일명의 확장자를 제거하고 서버에서 설정한 확장자를 붙일지 여부|

### setNumberExMode(numberExMode)
엑셀에 포함될 숫자 형식 데이터를 '통화'나 '사용자정의'가 아닌 '숫자' 서식으로 다운로드합니다. 클라이언트의 `down2Excel` 옵션 `numberExMode`보다 우선 적용됩니다.

|파라미터|타입|필수|설명|
|---|---|---|---|
|numberExMode|`boolean`|필수|숫자 데이터를 '숫자' 서식으로 다운받을지 여부|

### setXlsxTempFolderMode(useXssfMode)
POI 라이브러리 사용 중 `XLSX` 형식 다운로드 시 임시폴더를 사용하지 않고 메모리에서 직접 다운받도록 설정합니다.   
메모리 사용량이 늘어나므로 임시폴더를 사용할 수 없는 환경에서만 권장합니다.

|파라미터|타입|필수|설명|
|---|---|---|---|
|useXssfMode|`boolean`|필수|임시폴더 사용 여부 설정|

### setExcelBuffer(rowBuffer)
엑셀(`XLSX`) 다운로드 시 **메모리에 유지할 행 수**를 설정합니다. 지정한 행 수만 메모리에 두고 나머지는 디스크로 내보내(flush) 워크북 메모리를 줄입니다.

|파라미터|타입|필수|설명|
|---|---|---|---|
|rowBuffer|`int`|필수|메모리에 유지할 행 수 (기본 `100`)|

> 기본값은 `100`이라 미설정이어도 스트리밍됩니다. 메모리 여유가 있으면 값을 키워(예: `500`~`1000`) 디스크 flush 횟수를 줄일 수 있습니다.

### setImageProcessType(typ)
엑셀 다운로드 시 포함된 이미지의 비율 처리 방식을 설정합니다.

|파라미터|타입|필수|설명|
|---|---|---|---|
|typ|`int`|필수|`0`: 셀의 가로/세로에 꽉차게<br/>`1`: 셀 중앙에 원본 크기로<br/>`2`: 원본 비율 유지하며 셀에 맞춤|

### setUseGroupTree(useGroupTree)
트리 사용 시트에서 트리 구조를 엑셀 파일에 반영할지 여부를 설정합니다.

|파라미터|타입|필수|설명|
|---|---|---|---|
|useGroupTree|`boolean`|필수|트리 구조 엑셀 반영 여부|

### setExcelRowHeight(excelRowHeight)
엑셀 문서의 행 높이를 설정합니다. 클라이언트에서 설정하는 `excelRowHeight`보다 우선 반영됩니다.

|파라미터|타입|필수|설명|
|---|---|---|---|
|excelRowHeight|`int`|필수|엑셀 행 높이 설정|

### setExcelHeaderRowHeight(excelHeaderRowHeight)
엑셀 문서의 헤더행 높이를 설정합니다. 클라이언트에서 설정하는 `excelHeaderRowHeight`보다 우선 반영됩니다.

|파라미터|타입|필수|설명|
|---|---|---|---|
|excelHeaderRowHeight|`int`|필수|엑셀 헤더행 높이 설정|

### setService(HttpServletRequest, HttpServletResponse)
request와 response를 할당합니다. (기본 생성자 사용 시에만 적용)

### setTempRoot(tempRoot)
템플릿 파일이 저장된 경로를 지정합니다. 지정하지 않으면 시트의 `TempFile`에 사용된 경로만 이용합니다.

|파라미터|타입|필수|설명|
|---|---|---|---|
|tempRoot|`String`|필수|템플릿 파일의 경로|

### setTextLine(textLine)
텍스트 파일의 행 구분자를 설정합니다. (시트의 `RowDelim` 설정이 우선 적용)

|파라미터|타입|필수|설명|
|---|---|---|---|
|textLine|`String`|필수|행 레코드 구분자 (default: `\n`)|

### setTextSpliter(textSpliter)
텍스트 파일의 열 구분자를 설정합니다. (시트의 `ColDelim` 설정이 우선 적용)

|파라미터|타입|필수|설명|
|---|---|---|---|
|textSpliter|`String`|필수|열 레코드 구분자 (default: `\t`)|

### setTreeChar(treeChar)
트리 레벨 문자를 설정합니다.

|파라미터|타입|필수|설명|
|---|---|---|---|
|treeChar|`String`|필수|트리 레벨 문자 (default: `…`)|

### setWebServerDomain(webServerDomain)
문서에 이미지가 포함된 경우 이미지의 Root 폴더/웹 서버 도메인을 설정합니다. 설정하지 않으면 현재 서버 도메인을 사용합니다.

|파라미터|타입|필수|설명|
|---|---|---|---|
|webServerDomain|`String`|필수|이미지가 포함된 도메인 경로|

## IBSheetLoad (업로드)

`XLS`, `XLSX`, `CSV`, `TXT` 파일을 로드합니다.

### 생성자
|생성자|설명|
|---|---|
|`IBSheetLoad()`|request/response 할당이 없으면 `setService`로 등록해야 합니다.|
|`IBSheetLoad(HttpServletRequest, HttpServletResponse)`|request와 response를 포함한 생성자|
|`IBSheetLoad(HttpServletRequest, HttpServletResponse, String)`|파일이 업로드될 임시 경로를 사용하는 경우에 설정합니다. 설정하지 않으면 웹 서버의 기본 tempDirectory를 사용합니다.|

### close()
업로드를 종료하고 메모리를 해제합니다.

### directLoadExcel()
업로드한 문서를 `List<Map<String, String>>` 형태로 반환합니다. (`DirectLoadExcel` 전용)

### loadFile(file)
업로드한 엑셀 파일을 IBSheet가 읽을 수 있도록 로드/파싱합니다.   
`getUploadFile()`로 받은 파일을 DRM 복호화 등으로 가공한 뒤 넘길 때 사용합니다. 파일 경로(`loadFile(path)`)나 인자 없이(`loadFile()`)도 호출할 수 있습니다.

|파라미터|타입|필수|설명|
|---|---|---|---|
|file|`java.io.File`|선택|로드할 파일 객체|
|path|`String`|선택|로드할 파일 경로|

### setData(data, filePath)
멀티파트/XSS 필터로 `request`가 먼저 소비되는 환경에서, 클라이언트가 보낸 시트 전문(`Data`)과 업로드된 엑셀 파일 경로를 함께 세팅합니다. `setService` 호출 **전에** 호출합니다.

|파라미터|타입|필수|설명|
|---|---|---|---|
|data|`String`|필수|클라이언트가 전송한 시트 전문(`Data`)|
|filePath|`String`|필수|업로드된 엑셀 파일의 경로|

```java
String data = request.getParameter("columnTag");
load.setData(data, tempFile.getAbsolutePath());   // setService 전에 세팅
load.setService(request, response);
```

### getExtendParam(key)
시트에서 전달한 `ExtendParam` 정보를 받습니다. (반환: `String`)

|파라미터|타입|필수|설명|
|---|---|---|---|
|key|`String`|필수|`ExtendParam`에 설정한 Key 값|

### getUploadFile()
업로드한 파일 객체를 반환합니다. (반환: `java.io.File`, 업로드 파일 객체)

### getUploadFileName()
업로드한 파일의 파일명을 반환합니다. (반환: `String`)

### getLoadError(errorCode, message)
업로드 처리 페이지(`LoadExcel.jsp` 등)의 `catch` 블록에서 에러를 클라이언트로 내려보낼 때 사용합니다.   
반환된 `byte[]`를 `OutputStream`으로 출력하면 클라이언트 `onImportFinish` 이벤트의 `result`(코드)와 `message`로 전달됩니다.   
`onImportFinish`에 내부적으로 정의된 오류 코드/메시지와 겹치지 않게 지정합니다.  
인자 없이 `getLoadError()`를 호출하면 기본 에러가, `getLoadError(message)`는 메시지만 지정하는 형태입니다.

|파라미터|타입|필수|설명|
|---|---|---|---|
|errorCode|`int`|선택|에러 코드|
|message|`String`|선택|사용자에게 표시할 커스텀 메시지|

```java
catch (IBSheetException e) {
    OutputStream out = response.getOutputStream();
    out.write(load.getLoadError(e.getErrorCode(), e.getErrorMessage()));
    out.flush();
}
```

### getLoadFinish(type, result, message)
업로드 처리에 **성공**했을 때 완료를 클라이언트로 알립니다.   
반환된 `byte[]`를 `OutputStream`으로 출력하면 `onImportFinish` 이벤트의 `result`(`0` 이상 = 정상)와 `message`로 전달됩니다.

|파라미터|타입|필수|설명|
|---|---|---|---|
|type|`String`|필수|처리 유형 (예: `"EXCEL"`)|
|result|`int`|필수|결과 코드 (`0` 이상 = 정상)|
|message|`String`|필수|완료 메시지|

```java
OutputStream out = response.getOutputStream();
out.write(load.getLoadFinish("EXCEL", 1, "업로드 완료"));
out.flush();
```

### sendDirectTo(url)
업로드한 문서를 `Map` 형태로 `SHEETDATA`라는 `HttpRequest` Attribute에 저장하고 특정 경로로 전달합니다.

|파라미터|타입|필수|설명|
|---|---|---|---|
|url|`String`|필수|데이터를 전달받을 페이지 경로|

### sendDirectToFP()
업로드한 문서를 `Map` 형태로 `SHEETDATA`라는 `HttpRequest` Attribute에 저장하고, 시트에서 전달받은 FP 경로로 전달합니다.

### setEncoding(encoding)
페이지의 인코딩을 설정합니다.

|파라미터|타입|필수|설명|
|---|---|---|---|
|encoding|`String`|필수|페이지 인코딩 타입 (`UTF-8`, `EUC-KR` 등)|

### setMarkupTagDeilmiter(startTag1, startTag2, closingTag1, closingTag2)
기본 마크업 태그 외에 별도의 태그를 사용할 때 설정합니다. `ibsheet.cfg`의 `MarkupTagDelimiter` 설정 값과 동일해야 합니다.

|파라미터|타입|필수|설명|
|---|---|---|---|
|startTag1|`String`|필수|Start Tag 시작 문자열 (default: `<`)|
|startTag2|`String`|필수|Start Tag 완료 문자열 (default: `>`)|
|closingTag1|`String`|필수|Closing Tag 시작 문자열 (default: `</`)|
|closingTag2|`String`|필수|Closing Tag 완료 문자열 (default: `>`)|

### setDelimMode(mode)
시트 문자열에 `STX(\u0002)`, `ETX(\u0003)`가 포함된 경우 설정합니다.

|파라미터|타입|필수|설명|
|---|---|---|---|
|mode|`boolean`|필수|`0`: STX, ETX 문자 사용 (default)<br/>`1`: 변형된 문자열 사용|

### setStrictHeaderMatch(strictHeaderMatch)
엄격하게 헤더 매치를 검사할지 여부를 설정합니다. 설정 시 시트 헤더가 엑셀에 하나라도 존재하지 않으면 데이터를 로드하지 않습니다.

|파라미터|타입|필수|설명|
|---|---|---|---|
|strictHeaderMatch|`boolean`|필수|엄격한 헤더 매칭 검사 여부|

### setDisallowDuplicatedHeader(disallow)
업로드한 엑셀 파일의 헤더 행에 중복된 컬럼명이 있으면 로드를 중단하고 예외를 발생시킬지 설정합니다. `true`로 설정하면 중복 헤더 시 `IBSheetException`(에러 코드 `-18`)이 발생해 `catch`로 처리할 수 있습니다.

|파라미터|타입|필수|설명|
|---|---|---|---|
|disallow|`boolean`|필수|중복 헤더 불허 여부|

> 서버모듈 `2.0.9` 이상에서 지원합니다.

### setMaxRows(maxRows)
`LoadExcel` 처리를 허용할 최대 행 수를 설정합니다. 로드하는 데이터가 지정한 행 수보다 많으면 에러를 발생시키고 처리가 종료됩니다.

|파라미터|타입|필수|설명|
|---|---|---|---|
|maxRows|`int`|필수|최대 행 수 설정|

### setMaxColumns(maxColumns)
`LoadExcel` 처리를 허용할 최대 열 수를 설정합니다. 로드하는 데이터가 지정한 열 수보다 많으면 에러를 발생시키고 처리가 종료됩니다.

|파라미터|타입|필수|설명|
|---|---|---|---|
|maxColumns|`int`|필수|최대 열 수 설정|

### setSkipEmptyRow(skipEmptyRow)
엑셀의 빈 행을 로드할지 여부를 설정합니다.

|파라미터|타입|필수|설명|
|---|---|---|---|
|skipEmptyRow|`boolean`|필수|빈 행 로드 여부|

### setMaxFileSize(maxFileSize)
업로드 가능한 최대 파일 사이즈를 설정합니다.

|파라미터|타입|필수|설명|
|---|---|---|---|
|maxFileSize|`long`|필수|업로드 가능한 최대 파일 사이즈|

### setService(HttpServletRequest, HttpServletResponse)
request와 response를 할당합니다. (기본 생성자 사용 시에만 적용)

### setTextSpliter(textSpliter)
텍스트 파일의 열 구분자를 설정합니다. (시트의 `ColDelim` 설정이 우선 적용)

|파라미터|타입|필수|설명|
|---|---|---|---|
|textSpliter|`String`|필수|열 레코드 구분자 (default: `\t`)|

### writeToBrowser()
업로드한 파일을 파싱해서 브라우저의 시트에 전달합니다.

### writeToStream(OutputStream)
업로드한 파일을 파싱해서 `OutputStream`으로 전달합니다.

## Print2Pdf (PDF 다운로드)

### 생성자
|생성자|설명|
|---|---|
|`Print2Pdf()`|request/response 할당이 없으면 `setService`로 등록해야 합니다.|
|`Print2Pdf(HttpServletRequest, HttpServletResponse)`|request와 response를 포함한 생성자|

### print()
생성된 문서를 브라우저를 통해 다운로드합니다.

### saveTo(path)
생성된 문서를 서버의 특정 폴더에 저장합니다.

|파라미터|타입|필수|설명|
|---|---|---|---|
|path|`String`|필수|저장할 서버 경로|

### setDPI(dpi)
생성될 PDF 문서의 해상도를 지정합니다. 값이 작을수록 크게 출력됩니다.

|파라미터|타입|필수|설명|
|---|---|---|---|
|dpi|`Integer`|필수|PDF 해상도 (default: `2000`, `50`~`32800`)|

### setFontFolder(path)
TTF 폰트 파일이 저장된 경로를 지정합니다. (PDF 한글 표시를 위해 한글 폰트 ttf가 필요)

|파라미터|타입|필수|설명|
|---|---|---|---|
|path|`String`|필수|폰트 파일이 저장된 경로|

### setPageEncoding(encoding)
페이지의 인코딩을 설정합니다.

|파라미터|타입|필수|설명|
|---|---|---|---|
|encoding|`String`|필수|페이지 인코딩 타입 (`UTF-8`, `EUC-KR` 등)|

### setRequest(HttpServletRequest, HttpServletResponse)
request와 response를 할당합니다. (기본 생성자 사용 시에만 적용)

## 서버모듈/라이브러리 버전 확인

배포된 서버모듈과 로드된 라이브러리(POI 등)의 버전을 서버 콘솔에 출력해 정상 배포 여부를 확인할 수 있습니다.

```jsp
<%
System.out.println(com.ibleaders.ibsheet8.util.Version.getVersion());
%>
```

정상이면 서버모듈 버전과 함께 POI 계열 jar의 경로/버전이 콘솔에 표시됩니다. 출력이 없거나 `ClassNotFoundException` / `NoClassDefFoundError`가 발생하면 해당 jar가 `WEB-INF/lib`에 없거나 버전이 맞지 않는 것이므로, 개발 환경과 동일한 jar를 배포하세요.

## Read More
- [엑셀파일 업로드/다운로드 appendix](/docs/appx/import-export)
- [down2Excel method](/docs/funcs/excel/down-to-excel)
- [loadExcel method](/docs/funcs/excel/load-excel)
- [down2Pdf method](/docs/funcs/excel/down-to-pdf)
- [directDown2Excel method](/docs/funcs/excel/direct-down-to-excel)
- [directLoadExcel method](/docs/funcs/excel/direct-load-excel)
- [Export cfg](/docs/props/cfg/export)
