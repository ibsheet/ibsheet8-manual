# exportDataBuffer ***(method)***

<!-- synonyms: 엑셀 버퍼링, 다중 시트 엑셀 다운로드, 여러 시트 엑셀, 워크시트 분리, export data buffer -->

> 여러 시트의 내용을 하나의 엑셀 파일에 다운로드할 때 사용합니다.  
> `exportDataBuffer(true)`로 시작하면 이후 각 시트의 [exportData](./export-data) 호출이 즉시 다운로드되지 않고 버퍼에 누적되며,   
> `exportDataBuffer(false)`로 종료하면 누적된 시트들이 한 엑셀 파일의 워크시트로 묶여 다운로드됩니다.  
> 하나의 시트를 컬럼별로 나눠 여러 워크시트로 다운로드하는 데도 활용할 수 있습니다.

<!--!
> 
> **<mark>주의</mark> : [UseSpreadSheet](/docs/props/cfg/use-spread-sheet) 기능에서는 지원되지 않습니다.**
!-->

### Syntax
```javascript
void exportDataBuffer( isBuffer );
```

### Parameters

|Name|Type|Required|Description|
|----------|-----|---|----|
|isBuffer|`boolean`|<span class='required'>필수</span>|버퍼링 여부<br>`0(false)`:버퍼링 사용 안함 (`default`)<br>`1(true)`:버퍼링 사용|


### Return Value
***none***

### Example
```javascript
//1. 일반적인 사용 방법
//버퍼링 시작
sheet1.exportDataBuffer(true);

//첫번째 시트 데이터 버퍼링
var param1 = {
        fileName:"여행경비 내역.xlsx",
        sheetName:"교통비"  //엑셀파일내 워크시트 명
};
sheet1.exportData(param1);

//두번째 시트 데이터 버퍼링
var param2 = {
        sheetName:"식비"    //엑셀파일내 워크시트 명
};
sheet2.exportData(param2);

//세번째 시트 데이터 버퍼링
var param3 = {
        sheetName:"숙박비/기타"    //엑셀파일내 워크시트 명
};
sheet3.exportData(param3);

//전체 시트 다운로드(실제 다운로드가 시작됨)
sheet1.exportDataBuffer(false);



//2. 하나의 시트에서 컬럼별로 나누어 엑셀파일을 생성
//버퍼링 시작
sheet.exportDataBuffer(true);

//4개 컬럼만 첫번째 워크시트로 다운
var param1 = {
        sheetName:"12분기",
        downCols:"1QTCost|1QTProfit|2QTCost|2QTProfit"
};
sheet.exportData(param1);

//나머지 컬럼을 두번째 워크시트로 다운
var param2 = {
        sheetName:"34분기 및 종합",
        downCols:"3QTCost|3QTProfit|4QTCost|4QTProfit|Total|Summary"
};
sheet.exportData(param2);

//버퍼링 종료 (실제 다운로드가 시작됨)
sheet.exportDataBuffer(false);
```

### Read More

- [exportData method](./export-data)
- [importData method](./import-data)
- [down2ExcelBuffer method](/docs/funcs/excel/down-to-excel-buffer)


### Since

|product|version|desc|
|---|---|---|
|core|8.1.0.24|기능 추가|
