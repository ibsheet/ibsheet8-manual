# ExcludeEmpty ***(col)***

<!-- synonyms: 빈 값 제외, 0 제외, 합계 제외, 평균 계산 제외, 소계 빈값 제외, exclude empty, ignore zero, exclude zero, empty exclude sum, avg exclude -->

> 합계, 소계/누계행의 평균 또는 건수 등의 계산시 0 또는 빈 값을 포함할지 여부를 설정합니다.

### 적용되는 기능
> [makeSubTotal](/docs/funcs/core/make-sub-total) 소계/누계 행의 평균(avgCols)/카운트(countCols)  
> [FormulaRow](/docs/props/col/formula-row) 평균(Avg)/카운트(Count)/최소(Min)  
> [GroupSubTotal](/docs/props/col/group-sub-total) 평균(Avg)/카운트(Count)/최소(Min)

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|0 또는 빈 값 포함 (`default`)|
|`1(true)`|0 또는 빈 값 포함 안 함|

### Example
```javascript
options.Cols = [
    ...
    {Type: "Int", Name: "Pvt_TSum", ExcludeEmpty: 1, ...},
    ...
];
```

### Read More
- [makeSubTotal method](/docs/funcs/core/make-sub-total)
- [FormulaRow col](/docs/props/col/formula-row)
- [UseGroupSubTotal cfg](/docs/props/cfg/use-group-sub-total)
- [GroupSubTotal col](/docs/props/col/group-sub-total)


### Since

|product|version|desc|
|---|---|---|
|core|8.1.0.45|기능 추가|
|core|8.1.0.46|빈 값 포함 추가|
|core|8.1.0.49|누계 계산 버그 수정 **(해당 버전부터 사용해주세요.)**|