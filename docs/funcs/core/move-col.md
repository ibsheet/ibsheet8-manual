# moveCol ***(method)***
> 지정한 열의 위치를 이동합니다.  
> 열의 순서를 코드에서 직접 변경할 때 사용합니다.  
> `tocol`을 공백(`""`)으로 설정하면 `right` 값에 따라 해당 영역(section)의 맨 앞 또는 맨 뒤로 이동합니다.  
> `CanColMove`, `CanMove` 설정과 관계없이 호출할 수 있습니다.

### Syntax
```javascript
boolean moveCol( col, tocol, right, norender );
```

### Parameters
|Name|Type|Required| Description |
|----------|-----|---|----|
|col|`string`|<span class='required'>필수</span>|이동할 열 이름|
|tocol|`string`|<span class='required'>필수</span>|이동 기준이 되는 열 이름|
|right|`boolean`|<span class='optional'>선택</span>|`tocol` 기준 이동할 위치<br>`0(false)`:좌측 이동(`default`)<br>`1(true)`:우측 이동|
|norender|`boolean`|<span class='optional'>선택</span><mark>(사용주의)</mark>|즉시 화면에 반영할 것인지 여부<br/>`0(false)`:즉시 반영 (`default`)<br/>`1(true)`:즉시 반영하지 않음<br/>※ true로 설정한 경우 이후 rerender()를 반드시 호출해야 합니다.|


### Return Value
***boolean*** : 정상적으로 이동되었는지 여부(인자가 잘못된 경우 `undefined` 반환)

### Example
```javascript
// CUSTOMER_NAME 열을 AMOUNT12 열의 오른쪽으로 이동
sheet.moveCol("CUSTOMER_NAME", "AMOUNT12", 1, 0);
```

### Read More
- [addCol method](./add-col)
- [CanColMove cfg](/docs/props/cfg/can-col-move)
- [CanMove col](/docs/props/col/can-move)
- [Section col](/docs/props/col/section)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
