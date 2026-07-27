# recalculateRows ***(method)***

<!-- synonyms: 재계산, 다중 행 재계산, 행 배열 재계산, Formula 재계산, recalculateRows -->

> 지정한 여러 행의 [Formula](/docs/props/col/formula) 및 [속성(attribute+Formula)](/docs/props/col/attribute-formula)를 재계산합니다.
>
> [calculate](./calculate)와 달리 시트 전체가 아닌 전달한 행 배열에 한정해 재계산하므로, 일괄 변경 후 부분 갱신이 필요한 경우에 유리합니다.
>
> 단일 행/셀을 대상으로 재계산하려면 [recalculate](./recalculate)를 사용하세요.

### Syntax
```javascript
void recalculateRows( rows );
```

### Parameters

|Name|Type|Required|Description|
|----------|-----|---|----|
|rows|mixed( `array` \| `object` )|<span class='required'>필수</span>|재계산 대상 행 배열 또는 단일 [데이터 로우 객체](/docs/appx/row-object)<br/>단일 행을 전달해도 동작하며, 내부적으로 배열로 변환되어 처리됩니다.|

### Return Value
***none***

### Example
```javascript
// 체크된 행만 재계산
var rows = sheet.getRowsByChecked("chk");
sheet.recalculateRows(rows);

// 외부에서 여러 행의 값을 직접 변경한 뒤 일괄 재계산
var rows = sheet.getDataRows();
for (var i = 0; i < rows.length; i++) {
    rows[i].Discount = 0.1;
}
sheet.recalculateRows(rows);

// 단일 행도 전달 가능 (recalculate(row)와 유사하게 동작)
sheet.recalculateRows(sheet.getFocusedRow());
```

### Read More
- [recalculate method](./recalculate)
- [calculate method](./calculate)
- [Formula col](/docs/props/col/formula)
- [attribute+Formula col](/docs/props/col/attribute-formula)
- [CanFormula row](/docs/props/row/can-formula)
- [CalcOrder row](/docs/props/row/calc-order)
- [getRowsByChecked method](./get-rows-by-checked)

### Since

|product|version|desc|
|---|---|---|
|core|8.4.0.4|기능 추가|
