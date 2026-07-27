# isFocused ***(method)***
> 특정 행이나 셀에 포커스가 있는지 확인합니다.



### Syntax
```js
boolean isFocused( row, col );
```

### Parameters

|Name|Type|Required| Description |
|----------|-----|---|----|
|row |`object`|<span class='required'>필수</span>|[데이터 로우 객체](/docs/appx/row-object)|
|col |`string`|<span class='optional'>선택</span>|열이름|

### Return Value
***boolean*** : 포커스 유무 (0:unfocused, 1:focused)

### Example
```javascript
//id가 AR33인 행에 포커스가 있는지 확인한다.
var isfo = sheet.isFocused(sheet.getRowById("AR33"));

//특정 셀에 포커스가 있는지 확인한다.
var isfo = sheet.isFocused(sheet.getRowById("AR5"), "CA_DSC" );
```

### Read More
- [focus method](./focus)
- [getCanFocus method](./get-can-focus)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
