# getFocusedRow ***(method)***

<!-- synonyms: getFocusedRow, get-focused-row, 포커스 행, 포커스 로우, 포커스된 행, 활성 행, 현재 행, 선택 행, focused, row, current -->

> 시트 내에 현재 포커스된 셀(또는 행)의 [데이터 로우 객체](/docs/appx/row-object)를 반환합니다.

### Syntax
```javascript
object getFocusedRow();
```

### Return Value
***row object*** : [데이터 로우 객체](/docs/appx/row-object)

### Example
```javascript
//현재 포커스된 셀의 데이터 로우 객체를 반환합니다.
var row = sheet.getFocusedRow();
```

### Read More

- [getFocusedCol method](./get-focused-col)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
