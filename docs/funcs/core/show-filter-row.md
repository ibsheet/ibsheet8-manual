# showFilterRow ***(method)***

<!-- synonyms: showFilterRow, show-filter-row, 필터, 필터행, 필터 행, 필터 조건, 표시, 보이기, filter, row, header -->

> 헤더행 바로 아래에 **필터행(Filter Row)을 표시합니다.**
>
> 필터행이 표시되면 각 열에 조건을 입력하여 데이터를 필터링할 수 있습니다.  
> 필터 기능에 대한 자세한 설명은 [ShowFilter](/docs/props/cfg/show-filter) 문서를 참고하세요.


### Syntax
```javascript
boolean showFilterRow();
```


### Return Value
***boolean*** : 필터 행 보임 여부 (필터 행이 이미 표시되어 있거나 표시할 수 없는 경우 `0(false)` 반환)

### Example
```javascript
// 필터 행을 표시합니다.
sheet.showFilterRow();
```

### Read More
- [DisableKeyWord cfg](/docs/props/cfg/disable-keyword)
- [showFilter cfg](/docs/props/cfg/show-filter)
- [hideFilterRow method](./hide-filter-row)
- [doFilter method](/docs/funcs/core/do-filter)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
