# setFormulaRowPosition ***(method)***
> `FormulaRow`(합계행)의 위치(하단(기본값), 상단)를 변경할 수 있습니다.

### Syntax
```javascript
void setFormulaRowPosition( pos, norender );
```

### Parameters


|Name|Type|Required| Description |
|----------|-----|---|----|
|pos |`number`|<span class='required'>필수</span>|`0`: 상단으로 이동 <br/> `1`: 하단으로 이동 (`default: 1`)|
|norender |`boolean`|<span class='optional'>선택</span><mark>(사용주의)</mark>|즉시 화면에 반영할 것인지 여부<br/>해당 기능을 사용한 뒤, 다른 동작을 실행 할 경우 `renderBody()`를 반드시 먼저 실행 해야 합니다.<br/>`0(false)`: 즉시 반영 (`default`)<br/>`1(true)`: 반영 안함<br/>|

### Return Value
***boolean*** : 설정 완료 여부

### Example
```javascript
//합계행을 상단으로 이동
sheet.setFormulaRowPosition( 0 );

//합계행을 하단으로 이동
sheet.setFormulaRowPosition({pos:1});
```

### Read More
- [FormulaRow col](/docs/props/col/formula-row)
- [setFormulaRow method](./set-formula-row)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
