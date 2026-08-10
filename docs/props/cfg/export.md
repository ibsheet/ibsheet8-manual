# Export ***(cfg)***

<!-- synonyms: 엑셀 서버 경로, 서버모듈 URL, Cfg.Export, jsp 경로, 다운로드 업로드 경로, export config -->

> [down2Excel](/docs/funcs/excel/down-to-excel), [loadExcel](/docs/funcs/excel/load-excel), [down2Text](/docs/funcs/excel/down-to-text) 등 서버 모듈을 사용하는 함수가 호출할 서버 파일(jsp / aspx)의 경로를 지정합니다.  
> 함수 호출 시 시트 정보와 데이터가 지정된 경로의 jsp/aspx 파일로 전송되고, 서버는 이 정보를 받아 엑셀 파일을 생성해 클라이언트로 반환하거나 업로드된 파일을 시트로 로드합니다.  
> `Url` 속성만 필수이며, 함수별로 다른 경로가 필요하면 아래 `*Url` 속성으로 개별 지정합니다.

### Type
`object`

### Options
|Name|Type|Description|
|---------|----|-----------|
|Url|`string`|서버 모듈 파일(`Down2Excel.jsp`, `LoadExcel.jsp` 등)이 위치한 디렉터리 경로 **(필수)**. 지정한 경로 아래에서 함수별 jsp/aspx 파일을 자동으로 호출합니다.|
|Down2ExcelUrl|`string`|[down2Excel](/docs/funcs/excel/down-to-excel) 호출 시 사용할 URL. 지정하면 `Url`보다 우선합니다.|
|LoadExcelUrl|`string`|[loadExcel](/docs/funcs/excel/load-excel) 호출 시 사용할 URL. 지정하면 `Url`보다 우선합니다.|
|DirectLoadExcelUrl|`string`|[directLoadExcel](/docs/funcs/excel/direct-load-excel) 호출 시 사용할 URL. 지정하면 `Url`보다 우선합니다.|
|Down2TextUrl|`string`|[down2Text](/docs/funcs/excel/down-to-text) 호출 시 사용할 URL. 지정하면 `Url`보다 우선합니다.|
|LoadTextUrl|`string`|[loadText](/docs/funcs/excel/load-text) 호출 시 사용할 URL. 지정하면 `Url`보다 우선합니다.|
|Down2PdfUrl|`string`|[down2Pdf](/docs/funcs/excel/down-to-pdf) 호출 시 사용할 URL. 지정하면 `Url`보다 우선합니다.|
|down2HwpxUrl|`string`|[down2Hwpx](/docs/funcs/excel/down-to-hwpx) 호출 시 사용할 URL. 지정하면 `Url`보다 우선합니다.|
|Ext|`string`|서버 파일의 확장자 지정. `"jsp"` 또는 `"aspx"` (`default: "jsp"`)|
|FilePath|`string`|[File](/docs/appx/file-type-upload) 타입 컬럼의 파일 저장 경로. 셀의 [Path](/docs/props/cell/path) 속성이 있으면 그 값이 우선합니다.|
<!--!
|Down2HmlUrl|`string`|[down2Hml](/docs/funcs/excel/down-to-hml) 함수 호출시 연결할 `URL`을 강제 지정<br>이 속성이 설정되면 위에 `Url` 속성은 무시되고, 이 속성으로 지정한 `URL`이 호출됩니다.|
|`[비공개 동작안됨]` DirectDown2ExcelUrl|`string`|[directDown2Excel](/docs/funcs/excel/direct-down-to-excel) 함수 호출시 연결할 `URL`을 강제 지정<br>이 속성이 설정되면 위에 `Url` 속성은 무시되고, 이 속성으로 지정한 `URL`이 호출됩니다.|
|`[비공개 동작안됨]` Relative|`boolean`|주소의 상대경로 유무. `false: 실제주소(절대경로)` / `true: ibsheet.js` 기준 상태경로|
|`[비공개 동작안됨]` Method|`string`|주소로 접근할때 통신방식을 지정 . `POST/GET(default: "GET")`|
|`[비공개 동작안됨]` Param|`object`|전송 받거나 보낼 데이터의 파라미터를 설정(`객체형`)|
|`[비공개 동작안됨]` Params|`string`|전송받거나 보낼 데이터의 파라미터를 설정(`문자열형`)|
|`[비공개 동작안됨]` Header|`object`|http 헤더에 사용자가 지정한 헤더 정보를 설정|
!-->

### Example
```javascript
// 1. Url 하나로 모든 함수가 같은 경로의 jsp/aspx를 호출
options.Cfg.Export = {
   Url: '/IBSheet/jsp/',         // 서버모듈 jsp/aspx 파일이 모여 있는 디렉터리
   FilePath: '/IBSheet/file/'    // 파일 타입 컬럼 저장 경로
};
// down2Excel() 호출 → "/IBSheet/jsp/Down2Excel.jsp" 호출
// loadExcel()  호출 → "/IBSheet/jsp/LoadExcel.jsp"  호출


// 2. down2Excel만 별도 URL로 지정 (개별 우선)
options.Cfg.Export = {
   Url: '/IBSheet/jsp/',                          // 그 외 함수는 이 경로 사용
   Down2ExcelUrl: '/api/export/Down2Excel.jsp'    // down2Excel은 이 URL로 호출
};
// down2Excel() 호출 → "/api/export/Down2Excel.jsp" 호출 (Url 무시)
// loadExcel()  호출 → "/IBSheet/jsp/LoadExcel.jsp"  호출


// 3. ASP.NET 환경 — Ext로 aspx 호출
options.Cfg.Export = {
   Url: '/IBSheet/aspx/',   // 디렉터리 경로
   Ext: 'aspx'              // 호출 파일 확장자를 aspx로 결정
};
// down2Excel() 호출 → "/IBSheet/aspx/Down2Excel.aspx" 호출
```

### Read More

- [down2Excel method](/docs/funcs/excel/down-to-excel)
- [loadExcel method](/docs/funcs/excel/load-excel)
- [down2Text method](/docs/funcs/excel/down-to-text)
- [loadText method](/docs/funcs/excel/load-text)
- [directDown2Excel method](/docs/funcs/excel/direct-down-to-excel)
- [directLoadExcel method](/docs/funcs/excel/direct-load-excel)
- [down2Hwpx method](/docs/funcs/excel/down-to-hwpx)
- [AutoExcelMode cfg](./auto-excel-mode)
- [Down2ExcelConfig cfg](./down-to-excel-config)
- [LoadExcelConfig cfg](./load-excel-config)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|excel|0.0.11|`Ext` 기능 추가|
|excel|8.1.0.85|`down2Hwpx` 기능 추가|
