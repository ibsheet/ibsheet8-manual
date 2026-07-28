# down2ExcelBuffer ***(method)***

<!-- synonyms: 여러 시트 엑셀 다운로드, 다중 워크시트 엑셀, excel buffer, 엑셀 버퍼 다운로드 -->

> 여러 시트의 내용을 하나의 엑셀 파일에 다운로드할 때 사용합니다.  
> `down2ExcelBuffer(true)`로 시작하면 각 시트에서 [down2Excel](./down-to-excel) 호출이 즉시 다운로드되지 않고 버퍼에 누적되며, `down2ExcelBuffer(false)`로 종료하면 누적된 시트들이 한 엑셀 파일의 워크시트로 묶여 다운로드됩니다.  
> 하나의 시트를 컬럼별로 나눠 여러 워크시트로 다운로드하는 데도 활용할 수 있습니다.

### Syntax
```javascript
void down2ExcelBuffer( isBuffer );
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
sheet1.down2ExcelBuffer(true);

//첫번째 시트 데이터 버퍼링
var param1 = {
        fileName:"여행경비 내역.xlsx",
        sheetName:"교통비"  //엑셀파일내 워크시트 명
};
sheet1.down2Excel(param1);

//두번째 시트 데이터 버퍼링
var param2 = {
        sheetName:"식비"    //엑셀파일내 워크시트 명
};
sheet2.down2Excel(param2);

//세번째 시트 데이터 버퍼링
var param3 = {
        sheetName:"숙박비/기타"    //엑셀파일내 워크시트 명
};
sheet3.down2Excel(param3);

//전체 시트 다운로드(실제 다운로드가 시작됨)
sheet1.down2ExcelBuffer(false);





//2. 하나의 시트에서 컬럼별로 나누어 엑셀파일을 생성
//버퍼링 시작
sheet.down2ExcelBuffer(true);

//4개 컬럼만 첫번째 워크시트로 다운
var param1 = {
        sheetName:"12분기",
        downCols:"1QTCost|1QTProfit|2QTCost|2QTProfit"
};
sheet.down2Excel(param1);

//나머지 컬럼을 두번째 워크시트로 다운
var param2 = {
        sheetName:"34분기 및 종합",
        downCols:"3QTCost|3QTProfit|4QTCost|4QTProfit|Total|Summary"
};
sheet.down2Excel(param2);

//버퍼링 종료 (실제 다운로드가 시작됨)
sheet.down2ExcelBuffer(false);
```

### Read More

- [down2Excel method](./down-to-excel)


### Since

|product|version|desc|
|---|---|---|
|excel|0.0.3|기능 추가|
