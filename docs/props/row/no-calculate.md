# NoCalculate ***(row)***
> 특정행에 대한 소계 또는 합계 계산 포함 여부를 설정합니다.  
> `1(true)`로 설정시 해당 행은 소계 또는 합계 계산에 포함되지 않습니다.  
> 동적으로 속성을 추가한 경우 [calculate](/docs/funcs/core/calculate)를 호출해야 소계가 재계산됩니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|소계/합계 계산 포함 (`default`)|
|`1(true)`|소계/합계 계산 제외|


### Example
```javascript
// 조회 데이터에 설정
{"data":[
    {"NoCalculate":1, "ColName1":"Value1", "ColName2":"Value2"},
    {"ColName1":"Value3", "ColName2":"Value4"}
]}

// 동적으로 속성 추가 후 소계 재계산
var row = sheet.getFocusedRow();
row.NoCalculate = 1;
sheet.calculate(true, false);
```

### Read More
- [makeSubTotal method](/docs/funcs/core/make-sub-total)
- [FormulaRow col](/docs/props/col/formula-row)
- [setFormulaRow method](/docs/funcs/core/set-formula-row)
- [calculate method](/docs/funcs/core/calculate)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.7|기능 추가|
