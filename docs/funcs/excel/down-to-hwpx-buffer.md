# down2HwpxBuffer ***(method)***

<!-- synonyms: 여러 시트 한글 다운로드, 다중 한글 표, HWPX buffer, 한글 버퍼 다운로드 -->

> 여러 시트의 내용을 하나의 한글(Hwpx) 파일에 다운로드할 때 사용합니다.  
> `down2HwpxBuffer(true)`로 시작하면 각 시트에서 [down2Hwpx](./down-to-hwpx) 호출이 즉시 다운로드되지 않고 버퍼에 누적되며, `down2HwpxBuffer(false)`로 종료하면 누적된 시트들이 호출 순서대로 한글 문서의 표로 그려집니다.  
> 템플릿 기능과 `down2Hwpx`의 `sheetField` 옵션을 함께 사용하면 원하는 위치에 원하는 표를 배치할 수 있습니다.

### Syntax
```javascript
void down2HwpxBuffer( isBuffer );
```

### Parameters

|Name|Type|Required|Description|
|----------|-----|---|----|
|isBuffer|`boolean`|<span class='required'>필수</span>|버퍼링 여부<br>`0(false)`:버퍼링 사용 안함 (`default`)<br>`1(true)`:버퍼링 사용|


### Return Value
***none***

### Example
```javascript

//1. 템플릿을 사용하지 않고 한글 파일에 여러개의 시트를 그리는 방법
//버퍼링 시작
sheet.down2HwpxBuffer(true);

//4개 컬럼만 한글 표로 다운
var param1 = {
        downCols:"1QTCost|1QTProfit|2QTCost|2QTProfit"
};
sheet.down2Hwpx(param1);

//나머지 컬럼을 두번째 다음 문장의 한글 표로 다운
var param2 = {
        downCols:"3QTCost|3QTProfit|4QTCost|4QTProfit|Total|Summary"
};
sheet.down2Hwpx(param2);

//버퍼링 종료 (실제 다운로드가 시작됨)
sheet.down2HwpxBuffer(false);

//2. 템플릿을 사용 하여 원하는 위치에 시트를 생성하는 방법.

//버퍼링 시작
sheet1.down2HwpxBuffer(true);

//첫번째 시트 데이터 버퍼링
var param1 = {
        fileName:"이력서.hwpx",
        //tempFile과 keyField는 첫번째에서만 설정.
        tempFile:"Resume.hwpx",
        keyField: {
                "name": "홍길동",
                "engName": "Hong Gil Dong"
        },
        sheetField : "sheet1"
};
sheet1.down2Hwpx(param1);

//두번째 시트 데이터 버퍼링
var param2 = {
        sheetField : "shee2"
};
sheet2.down2Hwpx(param2);

//세번째 시트 데이터 버퍼링
var param3 = {
        sheetField : "shee3"
};
sheet3.down2Hwpx(param3);

//네번째 시트 데이터 버퍼링
var param4 = {
        sheetField : "shee4"
};
sheet4.down2Hwpx(param4);


//전체 시트 다운로드(실제 다운로드가 시작됨)
sheet1.down2HwpxlBuffer(false);
```
* 템플릿 화면 예시

![image](/assets/imgs/Resume.png)


### Read More

- [down2Hwpx method](./down-to-hwpx)


### Since

|product|version|desc|
|---|---|---|
|core|8.1.0.85|Down2Hwpx 기능 추가|
|excel|1.1.2|Down2Hwpx 기능 추가|
|jar|1.0.0|Down2Hwpx 기능 추가|
