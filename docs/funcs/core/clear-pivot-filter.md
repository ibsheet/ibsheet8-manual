# clearPivotFilter ***(method)***

<!-- synonyms: 피벗 필터 초기화, 피벗 필터 제거, 피벗 필터 지우기, 피벗 시트 재생성, 필터 초기화, clear-pivot-filter, clearPivotFilter, clear pivot filter, reset pivot filter, remove pivot filter -->

> 피벗 필터가 적용된 경우 필터행의 내용을 초기화한 뒤, 원본 시트에 따라 다시 피벗 시트를 생성합니다. 

### Syntax
```javascript
void clearPivotFilter();
```

### Return Value
***none***

### Example
```javascript
//피벗 필터를 제거하고 다시 피벗 시트를 생성합니다.
pivotSheet_sheet.clearPivotFilter();
```

### Read More
- [doPivotFilter method](./do-pivot-filter)

### Since

|product|version|desc|
|---|---|---|
|core|8.2.0.1|기능 추가|
