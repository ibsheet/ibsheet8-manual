# getAttribute ***(method)***

> 특정 행,열,셀에 설정된 속성값을 확인합니다.  
> `row`를 `null`로 설정시 열에 설정한 속성값이 리턴됩니다.  
> `col`을 `null`로 설정시 행에 설정한 속성값이 리턴됩니다.  
> 전용 함수가 있는 속성은 전용 함수 사용을 권장합니다.  
> - [getCanEdit](/docs/funcs/core/get-can-edit), [getCanFocus](/docs/funcs/core/get-can-focus), [getType](/docs/funcs/core/get-type), [getFormat](/docs/funcs/core/get-format)

### Syntax
```javascript
mixed getAttribute( row, col, attr);
```

### Parameters

|Name|Type|Required|Description|
|----------|-----|---|----|
|row |`object`|<span class='optional'>선택</span>|[데이터 로우 객체](/docs/appx/row-object)|
|col |`string`|<span class='optional'>선택</span>|열이름|
|attr|`string`|<span class='optional'>선택</span>|확인하고자 하는 속성명|

### Return Value
***mixed ( `number` \| `string` )*** : 인자에 따라 행이나 열,셀의 속성 값을 리턴

### Example
```javascript
//특정 셀의 배경색 확인
var color = sheet.getAttribute(sheet.getFocusedRow(), sheet.getFocusedCol(), "Color");
console.log("현재 셀 배경색: " + color);

//합계 행의 셀의 글자색 확인
var fcolor =  sheet.getAttribute( sheet.getRowById("FormulaRow"), sheet.getFocusedCol(), "TextColor");
```

### Read More
- [setAttribute method](./set-attribute)
- [getCanEdit method](./get-can-edit)
- [getCanFocus method](./get-can-focus)
- [getType method](./get-type)
- [getFormat method](./get-format)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
