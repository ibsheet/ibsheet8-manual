# setTotalRowCount ***(method)***

<!-- synonyms: setTotalRowCount, set-total-row-count, 전체 행수, 행수 설정, 데이터 건수, 총 건수, 변경, 표시, total, row, count, set -->

> [InfoRowConfig cfg](/docs/props/cfg/info-row-config) 기능 사용시 표시되는 전체 데이터 행수를 변경합니다.
>
> DB에서 가저온 건수와 다르게 표시하고 싶을때 유용합니다.

### Syntax
```javascript
void setTotalRowCount ( count );
```

### Parameters
|Name|Type|Required| Description |
|----------|-----|---|----|
|count |`number`|<span class='required'>필수</span>|전체 데이터 행수로 표시할 숫자|

### Return Value
***none***

### Example
```javascript
// 전체 데이터 행수를 변경
sheet.setTotalRowCount ( 2000 );
```

### Read More
- [InfoRowConfig cfg](/docs/props/cfg/info-row-config)
- [getTotalRowCount method](./get-total-row-count)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.7|기능 추가|