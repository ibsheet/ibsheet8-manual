# importData ***(method)***

<!-- synonyms: 엑셀 업로드, 엑셀 가져오기, 클라이언트 엑셀 업로드, jszip 엑셀, xlsx 업로드, txt csv 업로드, import data, DRM, 문서보안, DRM 해제 -->

> 엑셀 파일의 내용을 시트로 불러옵니다. (브라우저에서 처리되는 클라이언트 기능)  
> 사용 전 `/plugins/jszip.min.js` 파일이 반드시 로드되어 있어야 합니다.  
> 함수를 호출하면 파일 선택 창이 나타나고, 사용자가 선택한 파일은 클라이언트에서 바로 처리됩니다.  
> 엑셀 데이터를 시트에 어떻게 매핑할지는 `mode` 옵션이 결정합니다. (기본값 `HeaderMatch` — 헤더 타이틀 매칭)  
> 지원하는 파일 형식은 **xlsx, txt, csv** 입니다. (구버전 `xls` 형식은 지원하지 않습니다.)

### Syntax
```javascript
void importData( param );
```

### Parameters

|Name|Type|Required| Description |
|----------|-----|---|----|
|append|`boolean`|<span class='optional'>선택</span>|시트의 기존 데이터를 뒤에 엑셀의 데이터를 추가할지 여부(`default: 0(false)`)<br/>설정을 하지 않으면 기존데이터는 모두 삭제한 후 엑셀의 데이터가 추가됨<br/> `주의` 해당 옵션은 `SearchMode:4,5 (서버페이징)` 모드에서는 사용할 수 없습니다.<br>`0(false)`:기존 데이터 제거 후 엑셀 데이터 추가 (`default`)<br>`1(true)`:기존 데이터에 엑셀 데이터 추가|
|fileExt|`string`|<span class='optional'>선택</span>|파일 선택창에서 허용하는 파일 확장자를 구분자("\|")로 연결하여 설정합니다. (`default: "xlsx"`)|
|mode|`string`|<span class='optional'>선택</span>| `"HeaderMatch"`, `"NoHeader"`, `"HeaderSkip"` 중에 하나의 문자열을 입력합니다.<br/>각 모드의 의미는 다음과 같습니다.<br/><ul><li>`"HeaderMatch"` : 시트의 헤더행 타이틀과 엑셀의 첫번째 행부터 타이틀을 비교해서 읽습니다.<br/>`startRow` 속성이 지정된 경우 `startRow`에서 지정한 행부터 헤더행의 개수만큼 읽어 비교합니다.</li><li>`"NoHeader"` : 헤더행이 없다고 가정하고 첫행부터 순서대로 각 열에 대입합니다.</li><li>`"HeaderSkip"` : 헤더행은 있지만 열비교를 하지 않고 좌측부터 순서대로 읽습니다. 시트 헤더행이 2개라면 엑셀의 위에서 두 행을 제외하고 그 아래부터 읽는 식입니다.</li></ul>(`default: "HeaderMatch"`)|
| next | `object` | <span dir="">선택</span> | [데이터 로우 객체](/docs/appx/row-object)<br>지정한 행 위에부터 데이터 `append`. (`append:1(true)`일때만 사용 가능) |
|startRow|`number`|<span class='optional'>선택</span>|엑셀에서 시트가 몇번째 행에서 시작하는지 설정합니다. 설정하지 않으면 엑셀의 첫번째 행부터 (1부터시작) 읽어 들임 (`default: 1`) (`xlsx에서만 지원`)|
|startCol|`number`|<span class='optional'>선택</span>|엑셀에서 시트가 몇번째 열에서 시작하는지 설정합니다. 설정하지 않으면 엑셀의 첫번째 열부터 (1부터시작) 읽어 들임 <br/> `mode: HeaderMatch`의 경우 (7,12)에 있는 시트를 찾을 때, `startRow: 7` 만 설정해 줘도 그 Row에 헤더길이만큼 텍스트를 보기 때문에 `startCol`을 설정할 필요가 없다.<br/> 만약, `startCol`을 사용할 경우, 엑셀에 있는 시트에 첫번째 컬럼부터 `startCol`이 시작하게 된다 (`default: 1`) (`xlsx에서만 지원`)|
|workSheetName|`string`|<span class='optional'>선택</span>|읽어들일 엑셀 파일의 워크시트 명을 설정합니다. 일치하는 워크시트 명이 없으면 첫번째 워크시트를 읽습니다.|
|workSheetNameStrict|`boolean`|<span class='optional'>선택</span>|workSheetName에 설정한 워크시트가 없는 경우 첫번째 워크시트를 로드하지 않고 -17 에러 코드를 반환합니다.<br>`0(false)`:workSheetName에 설정된 워크시트가 없는 경우 첫번째 워크시트를 로드 (`default`)<br>`1(true)`:workSheetName에 설정된 워크시트가 없는 경우  -17 에러 코드를 반환|
|workSheetNo|`number`|<span class='optional'>선택</span>|읽어들일 엑셀 파일의 워크시트 순번을 설정합니다. 설정하지 않으면 첫번째 워크시트를 읽습니다. (`default: 1`)|
|columnMapping|`string`|<span class='optional'>선택</span>|엑셀 컬럼 번호를 이용해서 시트의 열 순서에 따라 데이터를 로드하는 옵션입니다. 구분자("\|")로 연결하여 설정합니다.(1번부터 시작)<br/> `mode: HeaderMatch`에서 컬럼매핑을 사용 할 경우 `HeaderMatch`의 기능은 무시되고 `HeaderSkip` 처럼 사용됩니다 (`xlsx에서만 지원`)|
|colSeparator|`string`|<span class='optional'>선택</span>|열과 열 사이의 구분자 문자, txt 업로드 일 경우 (`default: \t(탭문자)`, csv 업로드 일 경우(`default: ,(콤마)`) 업로드되는 파일에 따라 기본 구분자가 변경됩니다. `(txt, csv에서만 지원)`|
|encoding|`string`|<span class='optional'>선택</span>|텍스트 파일의 인코딩 형식 지정`(txt, csv에서만 지원)` (`default: "utf-8"`)|
|endRow|`number`|<span class='optional'>선택</span>|엑셀에서 몇번째 행까지 읽어들일 지 설정합니다. 설정하지 않으면 끝까지 읽어들입니다. 0부터 시작합니다.|
|file|`object`|<span class='optional'>선택</span>|file 객체 또는 Blob 객체로 된 엑셀 데이터를 직접 읽어들입니다. (`xlsx에서만 지원`)<br/> 해당 인자를 사용하게 되면 파일 다이얼로그가 나타나지 않습니다.|
|uploadImage|`boolean`|<span class='optional'>선택</span>| 셀 위에 띄워진 이미지를 업로드할지 여부를 결정합니다. <br> `0(false)`: 셀 위에 띄워진 이미지를 업로드하지 않음 <br>`1(true)`:셀 위에 띄워진 이미지를 업로드함 (`default`) |
|skipSEQ|`boolean`|<span class='optional'>선택</span>|mode: `NoHeader`, `HeaderSkip`으로 데이터를 업로드할 때 SEQ 컬럼을 스킵하고 데이터를 업로드합니다. `columnMapping`을 설정한 경우에는 해당 인자가 동작하지 않습니다. (`default: 0`) |
<!--!
|`[비공개]`fileType|`string`|<span class='optional'>선택</span>|file 인자를 통하여 엑셀 데이터 업로드시 파일의 확장자를 명시해 줍니다. `(xlsx, csv, txt)` (`default: xlsx`)|
!-->


### Return Value
***none***

### Example
```javascript
// 워크시트이름이 sheet이고 mode: "HeaderMatch" 엑셀에 시트가 3번째 행에 있는 경우 업로드
var param = {startRow:3, mode:"HeaderMatch", workSheetName:"sheet"};
sheet.importData(param);

// mode: "HeaderSkip" 엑셀에 시트가 3번째 행과 3번째 열에 있는 경우 업로드
var param = {startRow:3, startCol:3, mode:"HeaderSkip"};
sheet.importData(param);

// mode: "NoHeader", workSheet순서가 4번째인 엑셀에 시트가 7번째 행과 3번째 열에 있는 경우 업로드
var param = {startRow:7, startCol:3, mode:"NoHeader", workSheetNo:4};
sheet.importData(param);

// 1~5번째 까지 있는 엑셀 컬럼을 시트에 3,4,5,2,1 순서로 업로드
var param = {columnMapping: "3|4|5|2|1"}
sheet.importData(param);

// 파일 확장자를 이용하여 텍스트 업로드
var param = {fileExt:"csv|txt"};
sheet.importData(param);
```

### Read More
- [exportData method](./export-data)
- [loadExcel method](/docs/funcs/excel/load-excel)
- [onSelectFile event](/docs/events/on-select-file)
- [onImportFinish event](/docs/events/on-import-finish)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.7|기능 추가|
|core|8.0.0.20|`endRow` 기능 추가, 파일 형식 내용 추가|
|core|8.1.0.20|`file` 기능 추가|
|core|8.1.0.33|`workSheetNameStrict` 기능 추가|
|core|8.2.0.14|`next` 기능 추가|
|core|8.3.0.22|`uploadImage` 기능 추가|
|core|8.3.0.45|`skipSEQ` 기능 추가|
<!--!
|`[비공개]`core|8.1.0.20| `fileType` 기능 추가|
!-->