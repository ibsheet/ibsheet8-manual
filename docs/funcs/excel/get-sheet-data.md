# getSheetData ***(method)***

<!-- synonyms: 시트 데이터 추출, JSON 추출, CSV 추출, sheet data, get sheet data -->

> 시트의 데이터를 인자의 형식(JSON 또는 CSV)으로 추출합니다.  
> 대상 컬럼을 설정하지 않은 경우 모든 컬럼을 대상으로 합니다.  
> 이 함수는 `/plugins/ibsheet-excel.js` 플러그인에 정의되어 있어 해당 스크립트 로드가 필요합니다.

### Syntax
```javascript
void getSheetData( param );
```

### Parameters

|Name|Type|Required|Description|
|----------|-----|---|----|
|type|`string`|<span class='optional'>선택</span>|시트 데이터를 `JSON`으로 추출할지, `CSV`로 추출할지 선택합니다. (`default: "json"`)|
|cols|`string`|<span class='optional'>선택</span>|추출할 컬럼을 지정합니다. 설정하지 않는 경우 모든 컬럼 데이터를 추출합니다. 보여지는 열만 추출하고 싶다면 `"Visible"`로 설정합니다.|
|colDelim|`string`|<span class='optional'>선택</span>|출력 대상의 컬럼 구분자를 지정합니다. `type`을 `CSV`로 지정한 경우만 사용 가능합니다. (`default: ","`)|
|rowDelim|`string`|<span class='optional'>선택</span>|출력 대상의 행 구분자를 설정합니다. `type`을 `CSV`로 지정한 경우만 사용 가능합니다. (`default: "\r\n"`)|
|newLine|`string`|<span class='optional'>선택</span>|셀 데이터에 개행이 포함되어 있는 경우 출력 데이터의 개행 구분자를 설정합니다. `type`을 `CSV`로 지정한 경우만 사용 가능합니다. (`default: "\r\n"`)|
|styleProperty|`boolean`|<span class='optional'>선택</span>|행과 셀의 스타일 속성값을 포함하여 추출할지 여부. `type`을 `JSON`으로 지정한 경우만 사용 가능합니다. (`default: 0`)|

### styleProperty로 추출되는 데이터

|Target|Property|Description|
|------|--------|-----------|
|Row|`CanEdit`|대상 행의 편집 허용 여부|
|Row|`Color`|대상 행의 배경색|
|Row|`TextColor`|대상 행의 폰트 색상|
|Cell|`CanEdit`|대상 셀의 편집 허용 여부|
|Cell|`Color`|대상 셀의 배경색|
|Cell|`TextColor`|대상 셀의 폰트 색상|
|Cell|`TextBold`|대상 셀의 폰트 굵게(Bold) 여부|
|Cell|`TextItalic`|대상 셀의 폰트 기울임(Italic) 여부|
|Cell|`TextUnderLine`|대상 셀의 폰트 밑줄(Underline) 여부|
|Cell|`TextStrike`|대상 셀의 폰트 취소선(Strike) 여부|
|Cell|`TextOverline`|대상 셀의 폰트 윗줄(Overline) 여부|
|Cell|`Text`|대상 셀의 작은 대문자(Small Caps) 여부|

### Return Value
***none***

### Example
```javascript
// JSON 형식으로 추출
sheet.getSheetData({type: "json"});

// CSV 형식으로 추출
sheet.getSheetData({type: "csv"});

// 보이는 컬럼만 JSON으로 추출
sheet.getSheetData({type: "json", cols: "Visible"});

// 스타일 속성 포함 JSON 추출
sheet.getSheetData({type: "json", styleProperty: 1});
```

### Read More

- [down2Excel method](./down-to-excel)
- [down2Text method](./down-to-text)
- [exportData method](/docs/funcs/core/export-data)
- [getSaveJson method](/docs/funcs/core/get-save-json)

### Since

|product|version|desc|
|---|---|---|
|excel|1.1.12|기능 추가|
