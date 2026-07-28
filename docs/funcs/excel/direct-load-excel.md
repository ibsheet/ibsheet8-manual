# directLoadExcel ***(method)***

<!-- synonyms: 엑셀 서버 직접 업로드, direct load excel, 대용량 엑셀 업로드, 엑셀 서버 저장, DB 직접 저장 -->

> 사용자가 선택한 엑셀 파일을 시트에 로드하지 않고 지정한 서버 측 페이지로 바로 전달합니다.  
> 엑셀 내용을 시트에 띄울 필요 없이 서버에서 직접 처리하는 경우 사용합니다.  
> 사용 전 [서버모듈 설치](/docs/appx/import-export)와 `/plugins/ibsheet-excel.js` 스크립트 로드가 필요합니다.  
> 이 함수를 호출하면 파일 선택 창이 나타나고, 사용자가 선택한 엑셀 파일이 `Cfg.Export` 속성에 지정한 `DirectLoadExcel.jsp`(또는 `DirectLoadExcel.aspx`)로 전달됩니다.   
> 이 jsp 파일이 엑셀을 파싱한 뒤 `extendParam`의 `FP` 인자로 지정한 서버 측 페이지로 데이터를 forward합니다.

![DirectLoadExcel 과정](/assets/imgs/directloadexcel_process.png)

업로드 실패 시 결과 코드와 메시지는 [onImportFinish](/docs/events/on-import-finish)의 `result`(음수 코드)와 `message`로 받습니다. 중계 페이지에서 조건에 따라 오류 메시지를 내보내는 방법은 [엑셀 서버 모듈 트러블슈팅](/docs/appx/excel-server-troubleshooting)을 참고하세요.


### Syntax
```javascript
void directLoadExcel( param );
```

### Parameters

|Name|Type|Required|Description|
|----------|-----|---|----|
|extendParam|`string`|<span class='optional'>선택</span>|전달할 parameter(querystring형식으로 작성, String 형태로 rquest.setAttribute("extendParam에 설정한 파라미터 이름")으로 담음)<br><mark>DirectLoadExcel.jsp에서 파싱한 정보를 처리할 서블릿(혹은 jsp)경로를 **FP**라는 이름으로 전달해야 함</mark>|
|fileExt|`string`|<span class='optional'>선택</span>|업로드 가능한 파일 확장자를 구분자("\|")로 연결하여 설정합니다. (`default: "xls\|xlsx"`)|
|mode|`string`|<span class='optional'>선택</span>| "HeaderMatch", "NoHeader", "HeaderSkip" 중에 하나의 문자열을 입력합니다.<br/>각 문자의 의미는 다음과 같습니다.<br/><ul><li>"HeaderMatch" : 시트의 헤더행의 타이틀과 엑셀의 첫번째 행부터 타이틀을 비교해서 읽습니다.<br/>  StartRow속성이 지정된 경우 StartRow에서 지정한 행부터 해더행의 개수만큼의 행을 읽어 비교합니다.</li><li>"NoHeader" : 헤더행이 없다고 가정하고 첫행부터 순서대로 각 열에 대입합니다.</li><li>"HeaderSkip" : 헤더행은 있지만 열비교를 하지 않고 좌측부터 순서대로 읽습니다. 시트의 헤더행의 2개라면 엑셀의 위에서 두개행을 제외하고 그 아래부터 읽는다고 생각하시면 됩니다.</li></ul>(`default: "HeaderMatch"`)|
|startRow|`number`|<span class='optional'>선택</span>|엑셀에서 시트가 몇번째 행에서 시작하는지 설정합니다. 설정하지 않으면 엑셀의 첫번째 행부터 (1부터시작) 읽어들임.|
|endRow|`number`|<span class='optional'>선택</span>|엑셀에서 시트가 몇번째 행까지 읽어들일지를 설정합니다. 설정하지 않으면 엑셀의 마지막 행까지 읽어들임.|
|workSheetName|`string`|<span class='optional'>선택</span>|읽어들일 엑셀 파일의 워크시트 명을 설정합니다. 일치하는 워크시트 명이 없으면 첫번째 워크시트를 읽습니다.|
|workSheetNo|`number`|<span class='optional'>선택</span>|읽어들일 엑셀 파일의 워크시트 순번을 설정합니다. 설정하지 않으면 첫번째 워크시트를 읽습니다.|
|reqHeader|`object`|<span class='optional'>선택</span>|서버 전송 헤더에 사용자가 지정한 헤더 정보를 설정합니다.|
|useXhr|`boolean`|<span class='optional'>선택</span>| xhr 통신을 이용해 엑셀 파일을 로드합니다.<br>`0(false)`:xhr 통신 사용 안함 (`default`)<br>`1(true)`:xhr 통신 사용|


### Return Value
***none***

### Example
```javascript
//FP로 최종 데이터를 받을 서블릿(혹은 jsp) 경로를 지정해야 함
var param = {
        startRow:5,
        workSheetName:"sheet4",
        extendParam:"year=2019&deptNo=0041&FP=./save/empExcelData.do"
        };
sheet.directLoadExcel(param);
```

```java
//directLoadExcel 자바 서버모듈 예시
List<Map<String, Object>> data = (List<Map<String, Object>>)request.getAttribute("SHEETDATA");	

Map<String, Object> header = (Map<String, Object>)data.get(0);
for (String key : header.keySet()) {
  System.out.print(key + "|");
}
System.out.println();
	
for (Map<String, Object> row : li) {
  for (String key : row.keySet()) {
    System.out.print(row.get(key) + "|");
  }
  System.out.println();
}
```

```cs
//directLoadExcel 닷넷 서버모듈 예시
List<Object> data = (List<Object>)this.Context.Items["sheetData"];

Dictionary<String, String> header = (Dictionary<String, String>)data[0];
foreach (String key in header.Keys) {
  System.Diagnotics.Debug.Write(key + "|");
}
System.Diagnotics.Debug.WriteLine();

foreach (Dictionary<String, String> row in data) {
  foreach (String key in row.Keys) {
    System.Diagnotics.Debug.Write(row[key] + "|");
  }
  System.Diagnotics.Debug.WriteLine();
}
```

### Read More
- [loadExcel method](./load-excel)
- [directDown2Excel method](./direct-down-to-excel)
- [importData method](/docs/funcs/core/import-data)
- [onSelectFile event](/docs/events/on-select-file)
- [onImportFinish event](/docs/events/on-import-finish)
- [엑셀 업로드/다운로드 설정 appendix](/docs/appx/import-export)
- [엑셀 서버 모듈 트러블슈팅 appendix](/docs/appx/excel-server-troubleshooting)
- [엑셀 DRM 처리 appendix](/docs/appx/excel-drm)
- [엑셀 비밀번호 설정 appendix](/docs/appx/excel-password)

### Since

|product|version|desc|
|---|---|---|
|excel|0.0.0|기능 추가|
|excel|0.0.8|`reqHeader` 기능 추가|
