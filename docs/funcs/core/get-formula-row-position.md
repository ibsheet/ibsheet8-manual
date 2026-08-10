# getFormulaRowPosition ***(method)***

<!-- synonyms: getFormulaRowPosition, get-formula-row-position, 합계행 위치, 수식행 위치, FormulaRow 위치, 합계 위치, 합계행 조회, 합계행 상하단, formula, row, position -->

> `FormulaRow`(합계행)의 위치 (하단(기본값), 상단) 값을 얻어 올 수 있습니다.

### Syntax
```javascript
number getFormulaRowPosition();
```

### Return Value
***number*** : FormulaRow의 위치 값

### Example
```javascript
//합계행의 위치를 가져옵니다.
var pos = sheet.getFormulaRowPosition();
```

### Read More
- [setFormulaRow method](./set-formula-row)
- [setFormulaRowPosition method](./set-formula-row-position)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
