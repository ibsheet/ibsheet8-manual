# CanFormula ***(row)***

<!-- synonyms: 행 수식 허용, 행 단위 Formula, 부분 행만 계산, calculate 대상 행, can formula -->

> 행 단위로 [Formula](/docs/props/col/formula)와 [attribute+Formula](/docs/props/col/attribute-formula) 계산을 활성화할지 여부를 설정합니다.  
> `Def.Row.CanFormula: 1`로 전체 행 일괄 적용하거나, 특정 행만 `CanFormula: 1`로 지정해 [calculate](/docs/funcs/core/calculate)로 부분 계산할 수 있습니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)` | Formula 동작 안 함 (`default`)|
|`1(true)` | Formula 동작 가능|

### Example
```javascript
// 전체 데이터행 Formula 허용 (가장 흔한 사용)
options.Def = {
    Row: { CanFormula: 1 }
};

// 또는 전체는 비활성화하고 특정 행만 부분 적용 (성능 최적화 등 특수 케이스)
options.Def = {
    Row: { CanFormula: 0 }
};
// 조회 후 특정 행만 활성화
sheet.getRowById("AR3")["CanFormula"] = 1;
sheet.getRowById("AR5")["CanFormula"] = 1;

// Formula 재계산
sheet.calculate(1, 1);
```

### Read More
- [Formula col](/docs/props/col/formula)
- [attribute+Formula col](/docs/props/col/attribute-formula)
- [attribute+Formula row](/docs/props/row/attribute-formula)
- [CalcOrder row](./calc-order)
- [calculate method](/docs/funcs/core/calculate)
- [recalculate method](/docs/funcs/core/recalculate)
- [recalculateRows method](/docs/funcs/core/recalculate-rows)
<!--!
- `[비공개]` [onAfterCalculate event](/docs/events/on-after-calculate)
- `[비공개]` [onBeforeCalculate event](/docs/events/on-before-calculate)
- `[비공개]` [onCalculateCell event](/docs/events/on-calculate-cell)
!-->

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
