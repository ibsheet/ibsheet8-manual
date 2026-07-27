# loadText ***(method)***

<!-- synonyms: 텍스트 업로드, txt 업로드, csv 업로드, load text, 텍스트 가져오기 -->

> txt 또는 csv 파일의 내용을 시트로 `import`합니다.  
> 사용 전 [서버모듈 설치](/docs/appx/import-export)와 `/plugins/ibsheet-excel.js` 스크립트 로드가 필요합니다.  
> 이 함수를 호출하면 파일 선택 창이 나타나고, 사용자가 선택한 txt/csv 파일이 `Cfg.Export` 속성에 지정한 `LoadText.jsp`(또는 `LoadText.aspx`)로 전달됩니다.  
> 이 jsp 파일이 파일을 파싱해 JSON 형태로 시트에 반환합니다.  
> 시트마다 반복 설정이 번거로우면 [IBSheet.CommonOptions](/docs/static/common-options)로 공통 적용할 수 있습니다.

### Syntax
```javascript
void loadText( param );
```

### Parameters

|Name|Type|Required| Description |
|----------|-----|---|----|
|append|`boolean`|<span class='optional'>선택</span>|시트의 기존 데이터를 뒤에 text파일의 내용을 추가할지 여부<br/>설정을 하지 않으면 기존데이터는 모두 삭제한 후 데이터가 추가됨.<br>`0(false)`:기존 데이터 제거 후 엑셀 데이터 추가 (`default`)<br>`1(true)`:기존 데이터에 엑셀 데이터 추가|
|fileExt|`string`|<span class='optional'>선택</span>|업로드 가능한 파일 확장자를 구분자("\|")로 연결하여 설정합니다. (`defualt: "txt|csv"`)|
|mode|`string`|<span class='optional'>선택</span>| `"HeaderMatch"`, `"NoHeader"`, `"HeaderSkip"` 중에 하나의 문자열을 입력합니다.<br/>각 문자의 의미는 다음과 같습니다.<br/><ul><li>`"HeaderMatch"` : 시트의 헤더행의 타이틀과 엑셀의 첫번째 행부터 타이틀을 비교해서 읽습니다.<br/></li><li>`"NoHeader"` : 헤더행이 없다고 가정하고 첫행부터 순서대로 각 열에 대입합니다.</li><li>`"HeaderSkip"` : 헤더행은 있지만 열비교를 하지 않고 좌측부터 순서대로 읽습니다. 시트의 헤더행의 2개라면 엑셀의 위에서 두개행을 제외하고 그 아래부터 읽는다고 생각하시면 됩니다.</li></ul>(`default: "HeaderMatch"`)|
|colSeparator|`string`|<span class='optional'>선택</span>|열과 열 사이의 구분자 문자 (`default: '\t'(탭문자)`)|
|encoding|`string`|<span class='optional'>선택</span>|텍스트 파일의 인코딩 형식 지정 (`default: "utf-8"`)|
|sendParam|`object`|<span class='optional'>선택</span>|텍스트 로드시 서버로 전달할 파라미터를 설정합니다.|
|reqHeader|`object`|<span class='optional'>선택</span>|서버 전송 헤더에 사용자가 지정한 헤더 정보를 설정합니다.|
|useXhr|`boolean`|<span class='optional'>선택</span>| xhr 통신을 이용해 파일을 로드합니다.<br>`0(false)`:xhr 통신 사용 안함 (`default`)<br>`1(true)`:xhr 통신 사용|
<!--!
|`[비공개]` maxFileSize|`string`|<span class='optional'>선택</span>|최대 업로드 가능한 파일 사이즈를 설정합니다. (MB단위이며 설정하지 않으면 무제한입니다.)|
!-->

### Return Value
***none***

### Example
```javascript
//text 파일 업로드
var param = {mode:"NoHeader", append:1};
sheet.loadText(param);
```

### Read More
- [loadExcel method](./load-excel)
- [down2Text method](./down-to-text)
- [importData method](/docs/funcs/core/import-data)
- [onSelectFile event](/docs/events/on-select-file)
- [onImportFinish event](/docs/events/on-import-finish)

### Since

|product|version|desc|
|---|---|---|
|excel|0.0.0|기능 추가|
|excel|0.0.8|`reqHeader` 기능 추가|
