# loadExcelBuffer ***(method)***

<!-- synonyms: 여러 시트 엑셀 업로드, 다중 워크시트 엑셀 업로드, excel buffer load -->

> 하나의 엑셀 파일에서 여러 시트로 한 번에 로드할 때 사용합니다.  
> `loadExcelBuffer(true)`로 시작하면 각 시트의 [loadExcel](./load-excel) 호출이 즉시 동작하지 않고 버퍼링되며, `loadExcelBuffer(false)`로 종료하면 파일 선택 창이 열리고 선택한 엑셀의 각 워크시트 내용이 시트들에 로드됩니다.

### Syntax
```javascript
void loadExcelBuffer( isBuffer );
```

### Parameters

|Name|Type|Required| Description |
|----------|-----|---|----|
|isBuffer|`boolean`|<span class='required'>필수</span>|버퍼링 여부<br>`0(false)`:버퍼링 사용 안함 (`default`)<br>`1(true)`:버퍼링 사용|


### Return Value
***none***

### Example
```javascript
//버퍼링 시작
sheet1.loadExcelBuffer(true);

//정규직 워크시트의 내용을 sheet1에 업로드
var param1 = {workSheetName:"정규직"};
sheet1.loadExcel(param1);

//비정규직 워크시트의 내용을 sheet1에 업로드
var param2 = {workSheetName:"비정규직"};
sheet2.loadExcel(param2);

//버퍼링 종료 (파일다이얼로그 오픈)
sheet1.loadExcelBuffer(false);
```

### Read More
- [loadExcel method](./load-excel)

### Since

|product|version|desc|
|---|---|---|
|excel|0.0.3|기능 추가|
