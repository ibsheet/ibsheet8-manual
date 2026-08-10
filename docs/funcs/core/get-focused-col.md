# getFocusedCol ***(method)***

<!-- synonyms: getFocusedCol, get-focused-col, 포커스 열, 포커스 컬럼, 포커스된 열, 활성 열, 현재 열, 포커스 열이름, focused, column, current -->

> 시트 내에 현재 포커스된 셀의 열이름을 반환합니다.

### Syntax
```javascript
string getFocusedCol();
```

### Return Value
***string*** : 열이름

### Example
```javascript
//현재 포커스된 셀의 열이름을 반환합니다.
var row = sheet.getFocusedCol();
```

### Read More

- [getFocusedRow method](./get-focused-row)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
