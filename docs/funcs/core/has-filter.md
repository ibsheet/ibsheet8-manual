# hasFilter ***(method)***
> 현재 시트에 **필터 조건이 설정되어 있는지 여부**를 반환합니다.
>
> 필터행 입력, `setFilter`, `doFilter` 등으로 필터가 설정된 경우 `true`를 반환합니다.  
> `clearFilter` 호출 또는 필터가 모두 해제된 경우 `false`를 반환합니다.


### Syntax
```javascript
boolean hasFilter();
```

### Return Value
***boolean*** : 필터 조건 설정 여부

### Example
```javascript
//필터 조건 설정 여부
var isFiltered = sheet.hasFilter();
```

### Read More
- [showFilter cfg](/docs/props/cfg/show-filter)
- [showFilterRow method](./show-filter-row)
- [clearFilter method](./clear-filter)
- [setFilter method](./set-filter)
- [doFilter method](./do-filter)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
