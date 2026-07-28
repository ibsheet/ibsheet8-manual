# down2Text ***(method)***

<!-- synonyms: 텍스트 다운로드, txt 다운로드, csv 다운로드, down to text, 시트 텍스트 내보내기, CSV 인젝션, 수식 인젝션, formula injection, csv injection, escapeCsvInjection -->

> 시트의 내용을 `txt` 또는 `csv` 파일로 다운로드합니다.  
> 사용 전 [서버모듈 설치](/docs/appx/import-export)와 `/plugins/ibsheet-excel.js` 스크립트 로드가 필요합니다.  
> 이 함수를 호출하면 `Cfg.Export` 속성에 지정한 `Down2Text.jsp`(또는 `Down2Text.aspx`)가 호출되며, 이 jsp 파일이 시트 정보(컬럼 정의 등)와 데이터를 받아 텍스트 파일을 생성해 클라이언트로 전송합니다.  
> 시트마다 반복 설정이 번거로우면 [IBSheet.CommonOptions](/docs/static/common-options)로 공통 적용할 수 있습니다.

### Syntax
```javascript
void down2Text( param );
```

### Parameters

|Name|Type|Required|Description|
|----------|-----|---|----|
|fileName|`string`|<span class='optional'>선택</span>|다운로드 받을 파일명입니다. 확장자를 설정하지 않으면 `txt` 파일로 다운로드 됩니다.|
|rowDelim|`string`|<span class='optional'>선택</span>|text파일을 만들때 행 구분자(기본은 줄넘김 문자: `"\r\n"`)
|colDelim|`string`|<span class='optional'>선택</span>|txt 다운로드 일 경우(`default: \t(탭문자)`, csv 다운로드 일 경우(`default: ,(콤마)` 업로드되는 파일에 따라 기본 구분자가 변경됩니다.
|downRows|`string`|<span class='optional'>선택</span>|다운로드 받을 행 인덱스(구분자 "\|"로 연결 ex: "1\|3\|4\|5\|7")|
|downCols|`string`|<span class='optional'>선택</span>|다운로드 받을 열 Name(구분자 "\|"로 연결 ex: "amt\|qty1\|qty2\|qty3\|years")|
|downHeader|`boolean`|<span class='optional'>선택</span>|헤더행을 다운로드 받을지 여부<br>`0(false)`:다운로드 시 헤더행 미포함<br>`1(true)`:다운로드 시 헤더행 포함 (`default`)|
|downSum|`boolean`|<span class='optional'>선택</span>|합계행도 다운로드 받을지 여부<br>`0(false)`:합계 행 다운로드 시 미포함<br>`1(true)`:합계 행 다운로드 시 포함 (`default`)|
|downTreeHide|`boolean`|<span class='optional'>선택</span>|tree를 사용하는 경우, 접혀진 행도 엑셀에 다운로드 할지 여부를 설정합니다.<br>`0(false)`:접혀진 행(자식노드)들 다운로드 대상 제외 (`default`)<br>`1(true)`:접혀진 행(자식노드)들 다운로드 대상 포함|
|reqHeader|`object`|<span class='optional'>선택</span>|서버 전송 헤더에 사용자가 지정한 헤더 정보를 설정합니다.|
|downloadEncoding|`string`|<span class='optional'>선택</span>|다운로드받는 텍스트 파일의 인코딩 형식을 지정합니다. UTF-8(BOM) 설정시 BOM을 삽입한 UTF-8 인코딩 형식으로 텍스트 파일을 다운로드합니다. (`default: "txt: UTF-8, csv: EUC-KR"`)|
|extendParam|`string`|<span class='optional'>선택</span>|서버로 전달해야 하는 내용이 있는 경우 `GET` 방식의 `QueryString`으로 연결하여 서버로 같이 전달됩니다.<br/> (ex: `sheet.down2Excel({extendParam: "sido=서울시&sigungu=관악구"}`)|
|extendParamMethod|`string`|<span class='optional'>선택</span>|`extendParam`의 내용을 `GET` 또는 `POST`로 전달할지를 설정합니다.(`default: "GET"`)|
|useXhr|`boolean`|<span class='optional'>선택</span>| xhr 통신을 이용해 파일을 다운로드받습니다.<br>`0(false)`:xhr 통신 사용 안함 (`default`)<br>`1(true)`:xhr 통신 사용|
|escapeCsvInjection|`boolean`|<span class='optional'>선택</span>|CSV 다운로드 시 CSV 인젝션(수식 인젝션) 방어를 활성화합니다. `csv` 형식에서만 동작하며, `txt`에서는 값과 무관하게 무시됩니다.<br/>`1(true)`로 설정하면 위험 선두 문자로 시작하는 문자열 셀 값 앞에 작은따옴표(`'`)를 붙여 스프레드시트가 값을 수식이 아닌 텍스트로 인식하도록 강제합니다.<br/>방어 대상 선두 문자: `=`, `+`, `-`, `@`, 탭(`\t`), CR(`\r`), LF(`\n`), `\|`, `%`<br/>`0(false)`:방어 미적용, 셀 값을 원본 그대로 CSV에 기록 (`default`)<br/>`1(true)`:위험 선두 문자로 시작하는 값에 `'` prefix 부여<br/>사용자 입력이 그대로 CSV로 내려가고, 그 파일을 제3자가 열 가능성이 있는 화면에서 켜는 것을 권장합니다. `(csv에서만 지원)`|
<!--!
|`[비공개]` downCombo|`string`|<span class='optional'>선택</span>|`Enum` 타입의 선택 항목을 `Enum` 속성과 `EnumKeys` 속성 어떤 형태로 다운로드를 받을 지 설정합니다.<br/> `TEXT`: `Enum` 속성을 사용하여 다운로드합니다. (`default`)<br/> `CODE`: `EnumKeys` 속성을 사용하여 다운로드합니다.|
!-->

### Return Value
***none***

### Example
```javascript
//1. text 확장자로 다운로드
sheet.down2Text({fileName:"yearsProfit.txt"});


//2. csv 확장자로 다운로드
sheet.down2Text({fileName:"yearsProfit.csv", colDelim:","});

//3. csv 다운로드 + CSV 인젝션 방어
//   셀 값이 `=1+1`, `+82-10-...`, `@SUM(...)`처럼 위험 선두 문자로 시작하면
//   파일에 `'`가 prefix되어 저장되고, 엑셀에서 텍스트로 표시됩니다.
sheet.down2Text({fileName:"safe.csv", escapeCsvInjection: 1});
```

### downloadEncoding 설정시 유의사항 

![downloadEncoding_utf_8](/assets/imgs/downloadencoding_utf_8.png "downloadEncoding_utf_8")

`downloadEncoding`을 `UTF-8`로 설정해 csv 파일을 다운로드하시면 엑셀로 열였을 때 한글이 깨지는 현상이 발생합니다. <br>
엑셀로 열었을 때 한글이 깨지는 현상을 예방하면서 `UTF-8` 인코딩을 적용하기 위해서는 `downloadEncoding`을 `UTF-8(BOM)`으로 설정해주세요 (서버모듈 1.1.18 버전 이후 설정 가능).

### csv 다운로드시 기본 인코딩에 관해 

엑셀 플러그인 1.0.21 버전 이후로 csv 다운로드시 기본 인코딩 형식이 EUC-KR에서 UTF-8(BOM)으로 변경되었습니다. <br>
그런데 해당 인코딩 형식은 서버모듈 1.1.18 버전 이후로 지원되는 형식이기에, 엑셀 플러그인 1.0.21 버전을 사용하시며 down2Text 기능을 사용하시려면 반드시 서버모듈 버전을 1.1.18 버전 이후의 버전으로 업그레이드하시거나 downloadEncoding 옵션을 UTF-8(BOM) 이외의 값으로 별도 설정해주셔야 됩니다.

### Read More
- [AutoExcelMode cfg](/docs/props/cfg/auto-excel-mode)
- [down2Excel method](./down-to-excel)
- [down2Pdf method](./down-to-pdf)
- [exportData method](/docs/funcs/core/export-data)
- [loadText method](./load-text)
- [onBeforeExport event](/docs/events/on-before-export)
- [onExportFinish event](/docs/events/on-export-finish)

### Since

|product|version|desc|
|---|---|---|
|excel|0.0.0|기능 추가|
|excel|0.0.8|`reqHeader` 기능 추가|
|servermodule|1.1.18|`downloadEncoding: UTF-8(BOM)` 설정 추가|
|excel|1.0.21|csv 다운로드시 디폴트 인코딩 형식 `EUC-KR`에서 `UTF-8(BOM)`으로 변경 |
|excel|1.1.38|`escapeCsvInjection` 설정 추가 (csv 형식 전용)|
|servermodule|2.1.4|`escapeCsvInjection` 설정 추가 (csv 형식 전용)|