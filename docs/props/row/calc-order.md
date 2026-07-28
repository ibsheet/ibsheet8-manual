# CalcOrder ***(row)***

<!-- synonyms: 계산 순서, formula 순서, calc order, 의존 순서, 컬럼 계산 순서 -->

> [Formula](/docs/props/col/formula)와 [attribute+Formula](/docs/props/col/attribute-formula)가 적용된 컬럼의 `Name`(또는 `Name+속성명`)을 계산 순서대로 `,`로 연결한 문자열로 정의합니다.

### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`string`|계산 순서에 맞게 열이름(또는 열이름+속성명, 속성명)을 ","를 구분자로 연결한 문자열|

### 주의 사항

Formula 종류에 따라 CalcOrder 형식이 다릅니다.

| Formula 종류 | CalcOrder 형식 | 예 |
|---|---|---|
| 일반 [Formula](/docs/props/col/formula) (col) | 열이름 | `"yearSum,total"` |
| [attribute+Formula (col)](/docs/props/col/attribute-formula) | 열이름+속성명 | `"yearSumColor,rateCanEdit"` |
| [attribute+Formula (row)](/docs/props/row/attribute-formula) | 속성명만 | `"Color,CanEdit"` |

> - [CanFormula](./can-formula)가 `1`로 설정되어야 동작합니다.
> - 항목 사이에 공백이 들어가면 인식되지 않습니다. `"a, b, c"`가 아니라 `"a,b,c"`.
> - 일반 Formula만 사용하면 CalcOrder 없이도 동작하지만, attribute+Formula와 함께 쓸 때는 일반 Formula의 열이름도 CalcOrder에 포함해야 합니다.

### Example
```javascript
options.Def.Row = {
    CanFormula: 1,                                            // Formula 활성화 (필수)
    CalcOrder: "SubTotal,SubTotalColor"                       // 먼저 SubTotal, 다음 SubTotalColor 순서로 계산
    //          └─ Name (일반 Formula)
    //                   └─ Name+속성명 (attribute+Formula)
};

options.Cols = [
    {Type:"Int", Name:"QT1"},
    {Type:"Int", Name:"QT2"},
    {Type:"Int", Name:"SubTotal",
        Formula:"QT1+QT2",                                         // 일반 Formula — SubTotal 값
        ColorFormula:"Value > 500 ? '#FF0000' : '#333333'"}   // attribute+Formula — SubTotal 결과 기반 색상
];
```

### Read More

- [CanFormula row](./can-formula)
- [Formula col](/docs/props/col/formula)
- [attribute+Formula col](/docs/props/col/attribute-formula)
- [attribute+Formula row](/docs/props/row/attribute-formula)
- [calculate method](/docs/funcs/core/calculate)
- [recalculate method](/docs/funcs/core/recalculate)
- [recalculateRows method](/docs/funcs/core/recalculate-rows)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
