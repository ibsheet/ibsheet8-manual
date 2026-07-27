# hideFilterRow ***(method)***
> 필터 행(Filter Row)을 감춥니다.
>
> 필터 행을 감추면 화면에서 필터링이 해제되어 모든 행이 다시 표시됩니다.  
> 단, 필터 행에 입력된 값은 내부적으로 유지되며 다시 [showFilterRow](./show-filter-row) 호출 시  
> 이전에 입력된 필터 값이 표시되고 해당 필터가 다시 적용됩니다.


### Syntax
```javascript
boolean hideFilterRow( );
```

### Return Value
***boolean***   
필터 행이 감춰졌는지 여부를 반환합니다.  
이미 필터 행이 숨겨져 있거나 숨길 수 없는 경우 0(false)를 반환합니다.

### Example
```javascript
//필터행을 감춥니다.
sheet.hideFilterRow( );
```

### Read More
- [showFilter cfg](/docs/props/cfg/show-filter)
- [showFilterRow method](./show-filter-row)
- [clearFilter method](./clear-filter)
- [hasFilter method](./has-filter)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
