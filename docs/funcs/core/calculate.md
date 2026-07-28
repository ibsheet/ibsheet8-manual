# calculate ***(method)***

<!-- synonyms: 수식 계산, Formula 계산, 재계산, 소계 재계산, calculate -->

> 시트에 설정된 [Formula](/docs/props/col/formula) 및 [속성(attribute+Formula)](/docs/props/col/attribute-formula) 계산을 시트 전체에 대해 실행합니다.  
> 부분 재계산이 필요한 경우 [recalculate](./recalculate) 또는 [recalculateRows](./recalculate-rows)를 사용하세요.


### Syntax
```javascript
void calculate( render, calconly, fixedonly );
```

### Parameters


|Name|Type|Required|Description|
|----------|-----|---|----|
|render |`boolean`|<span class='optional'>선택</span>|Formula 컬럼 화면 반영 여부 (일반 컬럼은 `rerender()` 별도 호출 필요)<br/>`0(false)`:반영 안 함<br/>`1(true)`:Formula 컬럼만 즉시 반영 (`default`)|
|calconly|`boolean`|<span class='optional'>선택</span>|`Row.CanFormula = 1` 인 행만 계산할 지 여부<br/>`0(false)`:전체 행 계산 (`default`)<br/>`1(true)`:`Row.CanFormula = 1` 인 행들만 계산|
|fixedonly |`boolean`|<span class='optional'>선택</span>|`Fixed` 행들(`Header, Filter, FormulaRow`)만 계산할지 여부<br/>`0(false)`:전체 행 계산 (`default`)<br/>`1(true)`:`Fixed` 행들(`Header, Filter, FormulaRow`)만 계산|

> 일반 + Formula 컬럼 모두 변경 시 `calculate(true)` + `rerender(1)`은 렌더 2회 발생.  
> **`calculate(false)` + `rerender(1)`로 일괄 반영**이 성능상 유리.

### Return Value
***none***

### Example
```javascript
// 외부에서 여러 행의 값을 일괄 변경 후 시트 전체 재계산
// setValue를 calc:0/render:0으로 호출 → 마지막에 calculate + rerender로 일괄 마무리
var rows = sheet.getDataRows();
for (var i = 0; i < rows.length; i++) {
    sheet.setValue({row: rows[i], col: "Discount", val: 0.1, calc: 0, render: 0});
}
sheet.calculate(false, false);   // Formula 계산만 (render=true면 Formula 컬럼만 반영 → 렌더 2회 발생)
sheet.rerender(1);               // 모든 변경 화면 일괄 반영 (렌더 1회로 마무리)
```

### Read More

- [Formula col](/docs/props/col/formula)
- [attribute+Formula col](/docs/props/col/attribute-formula)
- [attribute+Formula row](/docs/props/row/attribute-formula)
- [CanFormula row](/docs/props/row/can-formula)
- [CalcOrder row](/docs/props/row/calc-order)
- [NoCalculate row](/docs/props/row/no-calculate)
- [FormulaRow col](/docs/props/col/formula-row)
<!--!
- `[비공개]` [onAfterCalculate event](/docs/events/on-after-calculate)
- `[비공개]` [onBeforeCalculate event](/docs/events/on-before-calculate)
- `[비공개]` [onCalculateCell event](/docs/events/on-calculate-cell)
!-->

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.0.0.8|`render` 인자 `default` 값 변경(`false -> true`)|
|core|8.0.0.11|`fixedonly` 추가|