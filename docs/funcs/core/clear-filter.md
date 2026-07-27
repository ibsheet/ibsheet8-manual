# clearFilter ***(method)***
> 시트에 **적용된 모든 필터를 해제**하고 **필터행(Filter Row)에 입력된 값을 초기화**합니다.  
> 필터는 `필터행 입력`, `setFilter`, `doFilter` 등 어떤 방식으로 적용된 경우에도 모두 해제됩니다.

### Syntax
```javascript
boolean clearFilter();
```

### Return Value
***boolean***    
필터행에 입력된 값이 있어 초기화가 수행된 경우 `true`를 반환합니다.  
필터행이 없거나 초기화할 값이 없는 경우 `false`를 반환합니다.

### Example
```javascript
//필터 초기화
sheet.clearFilter();
```

### Read More
- [showFilter cfg](/docs/props/cfg/show-filter)
- [showFilterRow method](./show-filter-row)
- [hideFilterRow method](./hide-filter-row)
- [doFilter method](./do-filter)
- [setFilter method](./set-filter)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
