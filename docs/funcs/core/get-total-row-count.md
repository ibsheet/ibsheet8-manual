# getTotalRowCount ***(method)***

<!-- synonyms: getTotalRowCount, get-total-row-count, 전체 행 수, 총 행 수, 행 개수, 로우 카운트, 데이터 건수, 개수 조회, total, row, count -->

> [SearchMode](/docs/props/cfg/search-mode) 0, 1에서는 현재 시트의 실제 행 수를 리턴합니다.  
> SearchMode 2에서는 조회 데이터에 `Total` 값이 있으면 `Total` 값을, 없으면 실제 행 수를 리턴합니다.  
> SearchMode 3~5에서는 조회 데이터의 `Total` 값을 리턴합니다.  
> 필터링 여부와 관계없이 값이 변하지 않습니다.

### Syntax
```javascript
number getTotalRowCount();
```

### Return Value
***number*** : 실제 행 수 또는 조회 데이터의 `Total` 값

### Example
```javascript
var total = sheet.getTotalRowCount();    // 전체 데이터 건수
var loaded = sheet.getDataRows().length; // 현재 시트에 로드된 행 수
```

### Read More
- [SearchMode cfg](/docs/props/cfg/search-mode)
- [페이징 응답 규격](/docs/dataStructure/paging-structure)
- [getDataRows method](./get-data-rows)
- [getShownRows method](./get-shown-rows)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
