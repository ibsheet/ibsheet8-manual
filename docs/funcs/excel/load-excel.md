# loadExcel ***(method)***

<!-- synonyms: 엑셀 업로드, 엑셀 가져오기, load excel, 서버 엑셀 업로드, 엑셀 파싱, jsp 엑셀 업로드, DRM, 문서보안, DRM 복호화, DRM 해제 -->

> 엑셀 파일의 내용을 시트로 `import`합니다.  
> 사용 전 [서버모듈 설치](/docs/appx/import-export)와 `/plugins/ibsheet-excel.js` 스크립트 로드가 필요합니다.  
> 이 함수를 호출하면 파일 선택 창이 나타나고, 사용자가 선택한 엑셀 파일이 `Cfg.Export` 속성에 지정한 `LoadExcel.jsp`(또는 `LoadExcel.aspx`)로 전달됩니다.  
> 이 jsp 파일이 엑셀을 파싱해 JSON 형태로 시트에 반환합니다.  
> 시트마다 반복 설정이 번거로우면 [IBSheet.CommonOptions](/docs/static/common-options)로 공통 적용할 수 있습니다.  
> 엑셀 데이터를 시트에 어떻게 매핑할지는 `mode` 옵션이 결정합니다. (기본값 `HeaderMatch` — 헤더 타이틀 매칭)

업로드가 서버에서 실패하면 결과 코드와 오류 메시지는 [onImportFinish](/docs/events/on-import-finish)의 `result`(음수 코드)와 `message`로 전달됩니다.

### Syntax
```javascript
void loadExcel( param );
```

### Parameters

|Name|Type|Required| Description |
|----------|-----|---|----|
|append|`boolean`|<span class='optional'>선택</span>|시트의 기존 데이터를 뒤에 엑셀의 데이터를 추가할지 여부<br/>설정을 하지 않으면 기존데이터는 모두 삭제한 후 엑셀의 데이터가 추가됨.<br>`0(false)`:기존 데이터 제거 후 엑셀 데이터 추가 (`default`)<br>`1(true)`:기존 데이터에 엑셀 데이터 추가|
|fileExt|`string`|<span class='optional'>선택</span>|업로드 가능한 파일 확장자를 구분자("\|")로 연결하여 설정합니다. (`default: "xls|xlsx"`)|
|maxFileSize|`string`|<span class='optional'>선택</span>|최대 업로드 가능한 파일 사이즈. (MB단위이며 설정하지 않으면 무제한입니다.)|
|mode|`string`|<span class='optional'>선택</span>| `"HeaderMatch"`, `"NoHeader"`, `"HeaderSkip"`, `"FullLoad"` 중에 하나의 문자열을 입력합니다.<br/>각 모드의 의미는 다음과 같습니다.<br/><ul><li>`"HeaderMatch"` : 시트의 헤더행 타이틀과 엑셀의 첫번째 행부터 타이틀을 비교해서 읽습니다.<br/>`startRow` 속성이 지정된 경우 `startRow`에서 지정한 행부터 헤더행의 개수만큼 읽어 비교합니다.</li><li>`"NoHeader"` : 헤더행이 없다고 가정하고 첫행부터 순서대로 각 열에 대입합니다.</li><li>`"HeaderSkip"` : 헤더행은 있지만 열비교를 하지 않고 좌측부터 순서대로 읽습니다. 시트 헤더행이 2개라면 엑셀의 위에서 두 행을 제외하고 그 아래부터 읽는 식입니다.</li><li>`"FullLoad"` : 파일의 모든 워크시트를 'NoHeader' 모드로 업로드 다이얼로그에 로드합니다. (아래 설명 참고)</li></ul>(`default: "HeaderMatch"`)|
| next | `object` | <span dir="">선택</span> | [데이터 로우 객체](/docs/appx/row-object)<br>지정한 행 위에부터 데이터 `append`. (`append:1(true)`일때만 사용 가능) |
|startRow|`number`|<span class='optional'>선택</span>|엑셀에서 시트가 몇번째 행에서 시작하는지 설정합니다. 설정하지 않으면 엑셀의 첫번째 행부터 (1부터시작) 읽어들임.|
|startCol|`number`|<span class='optional'>선택</span>|엑셀에서 시트가 몇번째 열에서 시작하는지 설정합니다. 설정하지 않으면 엑셀의 첫번째 열부터 (1부터시작) 읽어들임. <br/> `mode: HeaderMatch`의 경우 (7,12)에 있는 시트를 찾을 때, `startRow: 7` 만 설정해 줘도 그 Row에 헤더길이만큼 텍스트를 보기 때문에 `startCol`을 설정할 필요가 없다. 만약, `startCol`을 사용할 경우, 엑셀에 있는 시트에 첫번째 컬럼부터 `startCol`이 시작하게 된다.|
|workSheetName|`string`|<span class='optional'>선택</span>|읽어들일 엑셀 파일의 워크시트 명을 설정합니다. 일치하는 워크시트 명이 없으면 첫번째 워크시트를 읽습니다.|
|workSheetNameStrict|`boolean`|<span class='optional'>선택</span>|workSheetName에 설정한 워크시트가 없는 경우 첫번째 워크시트를 로드하지 않고 -17 에러 코드를 반환합니다<br>`0(false)`:workSheetName에 설정된 워크시트가 없는 경우 첫번째 워크시트를 로드 (`default`)<br>`1(true)`:workSheetName에 설정된 워크시트가 없는 경우  -17 에러 코드를 반환|
|workSheetNo|`number`|<span class='optional'>선택</span>|읽어들일 엑셀 파일의 워크시트 순번을 설정합니다. 설정하지 않으면 첫번째 워크시트를 읽습니다.|
|columnMapping|`string`|<span class='optional'>선택</span>|엑셀 컬럼 번호를 이용해서 시트의 열 순서에 따라 데이터를 로드하는 옵션입니다. 구분자("\|")로 연결하여 설정합니다.(1번부터 시작) mode 속성값은 무시된다.|
|sendParam|`object`|<span class='optional'>선택</span>|엑셀 로드시 서버로 전달할 파라미터를 설정합니다.|
|endRow|`number`|<span class='optional'>선택</span>|엑셀에서 몇번째 행까지 읽어들일 지 설정합니다. 설정하지 않으면 끝까지 읽어들입니다. 0부터 시작합니다.|
|reqHeader|`object`|<span class='optional'>선택</span>|서버 전송 헤더에 사용자가 지정한 헤더 정보를 설정합니다.|
|skipEmptyRow|`boolean`|<span class='optional'>선택</span>|엑셀 로드 시 빈 행을 생략할 지 설정합니다.<br>`0(false)`:엑셀 로드 데이터에 빈 행 정보 포함<br>`1(true)`:엑셀 로드 데이터에 빈 행 정보 제외 (`default`)|
|workbookPassword|`string`|<span class='optional'>선택</span>| 읽어들일 엑셀 파일에 비밀번호가 설정된 경우 사용하는 옵션입니다. <br/>  xlsx 확장자 파일에서만 지원됩니다.|
|useXhr|`boolean`|<span class='optional'>선택</span>| xhr 통신을 이용해 엑셀 파일을 로드합니다.<br>`0(false)`:xhr 통신 사용 안함 (`default`)<br>`1(true)`:xhr 통신 사용|
|uploadImage|`boolean`|<span class='optional'>선택</span>| 셀 위에 띄워진 이미지를 업로드할지 여부를 결정합니다. <br> `0(false)`: 셀 위에 띄워진 이미지를 업로드하지 않음 <br>`1(true)`:셀 위에 띄워진 이미지를 업로드함 (`default`) |
|skipSEQ|`boolean`|<span class='optional'>선택</span>|mode: `NoHeader`, `HeaderSkip`으로 데이터를 업로드할 때 SEQ 컬럼을 스킵하고 데이터를 업로드합니다. `columnMapping`을 설정한 경우에는 해당 인자가 동작하지 않습니다. (`default: 0`) |
|activeSheet|`boolean`|<span class='optional'>선택</span>|엑셀 업로드시 활성화된 워크시트를 업로드합니다.|
<!--!
|`[비공개]` useDOM|`boolean`|<span class='optional'>선택</span>|자바 서버모듈에서 `xlsx` 형식의 엑셀 파일의 파싱 방법을 설정합니다.<br/>`0(false)`: SAX방식을 사용합니다. 이 방식은 대용량 처리에 적합합니다. 하지만, **서식 오류**가 생길 우려가 있습니다. (`default`)<br/>`1(true)`: DOM방식을 사용합니다. SAX방식에 비해 처리 속도는 느리지만, 서식에 맞게 로드가 가능합니다. 또한, `xls`와 `xlsx` 간의 호환성에도 유리합니다.|
!-->

### FullLoad 모드

![FullLoad 모드](/assets/imgs/loadexcel_mode_fullload.png "FullLoad 모드")

`FullLoad` 모드는 엑셀 업로드시 파일에 존재하는 모든 워크시트를 'NoHeader' 모드 상태로 업로드 다이얼로그에 로드하는 모드입니다. <br> 
로드된 워크 시트 중 한 가지를 선택한 뒤, 확인 버튼을 클릭해 선택된 워크 시트를 원본 시트에 로드하실 수 있습니다. <br>
**`FullLoad` 모드를 사용하시려면 반드시 다이얼로그 플러그인을 `1.0.11` 이후 버전으로, 서버모듈을 `1.1.21` 이후 버전으로, 엑셀 플러그인을 `1.0.21` 이후 버전으로 패치해주셔야 됩니다.**


### Return Value
***none***

### Example
```javascript
// 모드가 HeaderMatch, 엑셀이 5번째 로우의 위치, 워크시트 이름은 12월결산인 엑셀을 로드
var param = {startRow:5, mode:"HeaderMatch", workSheetName:"12월결산"};
sheet.loadExcel(param);

// 모드가 HeaderSkip, 엑셀이 4번째 로우, 3번째 컬럼부터 시작.
var param = {startRow:4, startCol:3, mode:"HeaderMatch"}
sheet.loadExcel(param);

// IBSheet의 첫번째 컬럼에 엑셀의 5번째 컬럼의 값을 로딩하고, IBSheet 의 5번째 컬럼에 엑셀의 1번째 컬럼의 값을 로딩
sheet.loadExcel({columnMapping:"5|4|3|2|1"});
```

### Read More
- [LoadExcelConfig cfg](/docs/props/cfg/load-excel-config)
- [loadExcelBuffer method](./load-excel-buffer)
- [importData method](/docs/funcs/core/import-data)
- [loadText method](./load-text)
- [down2Excel method](./down-to-excel)
- [down2Text method](./down-to-text)
- [onImportFinish event](../events/on-import-finish)
- [onSelectFile event](../events/on-select-file)
- [엑셀 업로드/다운로드 설정 appendix](/docs/appx/import-export)
- [엑셀 서버 모듈 트러블슈팅 appendix](/docs/appx/excel-server-troubleshooting)
- [엑셀 DRM 처리 appendix](/docs/appx/excel-drm)
- [엑셀 비밀번호 설정 appendix](/docs/appx/excel-password)

### Since

|product|version|desc|
|---|---|---|
|excel|0.0.0|기능 추가|
|excel|0.0.8|`reqHeader` 기능 추가|
|excel|1.0.12|`workSheetNameStrict` 기능 추가|
|dialog|1.0.11|`FullLoad` 기능 추가 (`servermodule`: 1.1.21, `excel`: 1.0.21)|
|excel|1.1.8|`next` 기능 추가|
|excel|1.1.23|`uploadImage` 기능 추가 (`servermodule`: 2.0.2)|
|excel|1.1.31|`skipSEQ` 기능 추가 (`servermodule`: 2.0.13)|
|excel|1.1.32|`activeSheet` 기능 추가 (`servermodule`: 2.0.15)|
