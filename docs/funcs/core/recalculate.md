# recalculate ***(method)***

<!-- synonyms: 재계산, 부분 재계산, 셀 재계산, 행 재계산, Formula 재계산, recalculate -->

> 특정 행/셀의 [Formula](/docs/props/col/formula) 및 [속성(attribute+Formula)](/docs/props/col/attribute-formula)를 재계산합니다.
>
> [calculate](./calculate)와 달리 시트 전체가 아닌 지정한 대상과 연관된 행/셀만 재계산하므로, 부분 변경 후 빠른 갱신이 필요한 경우에 유리합니다.
>
> 여러 행을 한 번에 재계산하려면 [recalculateRows](./recalculate-rows)를 사용하세요.

### Syntax
```javascript
void recalculate( row, col );
```

### Parameters

|Name|Type|Required|Description|
|----------|-----|---|----|
|row|`object`|<span class='required'>필수</span>|재계산 대상 [데이터 로우 객체](/docs/appx/row-object)|
|col|`string`|<span class='optional'>선택</span>|재계산 대상 열이름<br/>생략 시 해당 행 전체를 대상으로 재계산|

### Return Value
***none***

### Example
```javascript
// 특정 행 전체 재계산
var row = sheet.getFocusedRow();
sheet.recalculate(row);

// 특정 행의 특정 셀만 재계산
sheet.recalculate(row, "Amount");

// 외부에서 값을 직접 변경한 뒤 재계산 (행 상태 변경 없이 화면만 갱신하는 패턴)
var row = sheet.getRowById("AR5");
row.Qty = 100;
sheet.recalculate(row, "Qty");
```

### Read More
- [calculate method](./calculate)
- [recalculateRows method](./recalculate-rows)
- [Formula col](/docs/props/col/formula)
- [attribute+Formula col](/docs/props/col/attribute-formula)
- [CanFormula row](/docs/props/row/can-formula)
- [CalcOrder row](/docs/props/row/calc-order)
- [setValue method](./set-value)

### Since

|product|version|desc|
|---|---|---|
|core|8.4.0.4|기능 추가|
