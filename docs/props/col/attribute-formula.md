# attribute+Formula ***(col)***

<!-- synonyms: 열 속성 수식, col attribute formula, 컬럼 속성 자동 계산, 셀 색상 수식, 셀 편집 가능 수식 -->

> 컬럼에 설정해 셀별로 배경색(`Color`), 편집 가능 여부(`CanEdit`), 텍스트 색(`TextColor`) 등의 속성을 조건에 따라 다르게 적용할 때 이용합니다.  
> [CanFormula](/docs/props/row/can-formula)가 `1`로 설정되어야 동작하며, [CalcOrder](/docs/props/row/calc-order)에 **`열이름+속성명`** 형식으로 정의해야 합니다.  
> 컬럼에 설정하지만 셀 단위로 실행되므로, 도움말 [properties → Cell](/docs/props/cell/) 카테고리에 정의된 셀 단위 속성만 `속성명Formula` 형식으로 사용할 수 있습니다.

### Type
`mixed`( `function` \| `string` )

### Options
|Value|Description|
|-----|-----|
|`string`|컬럼명·예약어를 식에 직접 사용한 수식 문자열 (예: `"Value > 100 ? '#FF0000' : '#FFFFAA'"`)|
|`function`|계산 결과를 `return`하는 함수 (return 값이 없으면 반영 안 됨)<br/>첫 번째 인자로 `fr` 객체가 자동 전달됨|

### Parameters

**function 형식** — 함수 인자 `fr`의 속성

|Name|Type|Description|
|---|---|---|
|`Sheet`|`object`|시트 객체|
|`Row`|`object`|행 객체|
|`Col`|`string`|Formula 설정한 컬럼명|
|`Attr`|`string`|Formula가 적용되는 `열이름+속성명` (예: `yearSumColor`, `rateCanEdit`)|
|`Value`|`mixed`|Formula 설정한 컬럼의 셀 값|

**string 형식** — 식 내 예약어

|Name|Type|Description|
|---|---|---|
|`Sheet`|`object`|시트 객체|
|`Row`|`object`|행 객체|
|`Col`|`string`|Formula 설정한 컬럼명|
|`Attr`|`string`|Formula가 적용되는 `열이름+속성명` (예: `yearSumColor`, `rateCanEdit`)|
|`Value`|`mixed`|Formula 설정한 컬럼의 셀 값|
|컬럼명|`mixed`|컬럼명을 직접 사용 시 해당 셀의 값 (예: `yearSum > 100`)|

### 주의 사항
> - [CanFormula](/docs/props/row/can-formula)를 설정하지 않으면 Formula가 동작하지 않습니다.
> - 속성(attribute+Formula)는 [CalcOrder](/docs/props/row/calc-order)가 항상 필요합니다.
> - [CalcOrder](/docs/props/row/calc-order)에 열이름이 빠지면 인식되지 않습니다. `"Color,CanEdit"`처럼 속성명만 적지 말고 `"yearSumColor,rateCanEdit"`처럼 열이름+속성명으로 적어야 합니다.
> - [CalcOrder](/docs/props/row/calc-order) 항목 사이에 공백이 들어가도 인식되지 않습니다. `"yearSumColor, rateCanEdit"`가 아니라 `"yearSumColor,rateCanEdit"`.
> - `TypeFormula`로 Type을 전환할 때는 새 Type이 요구하는 형식 속성(`Format`, `EditFormat`, `DataFormat` 등)과 원본 데이터 값도 함께 변환해야 합니다.

### Example
```javascript
options.Def.Row = {
    CanFormula: 1,
    // col attr+Formula의 CalcOrder는 "열이름+속성명" 형식, 항목 사이에 공백 없이
    CalcOrder: "yearSumColor,rateCanEdit"
};

options.Cols = [
    {Type: "Bool", Name: "CHK"},

    // string 형식 — Value 예약어로 자신의 셀 값 참조
    {Type: "Int", Name: "yearSum",
        ColorFormula: "Value > 100 ? '#FF0000' : '#FFFFAA'"
    },

    // function 형식 — fr 인자로 행 데이터 접근
    {Type: "Float", Name: "rate",
        CanEditFormula: function(fr) {
            return fr.Row["CHK"] == 1 && fr.Row["yearSum"] > 150;
        }
    }
];
```

### Try it
- [Demo of attribute+Formula (기본 — 셀별 색상, 편집 가능 여부 적용)](https://jsfiddle.net/gh/get/library/pure/ibsheet/ibsheet8-manual-sample/tree/master/samples/properties/Col/attributeFormula/)
- [Demo of attribute+Formula (TypeFormula — 셀별 숫자 포맷 변경)](https://jsfiddle.net/gh/get/library/pure/ibsheet/ibsheet8-manual-sample/tree/master/samples/properties/Col/attributeFormula-TypeChange-Numeric/)
- [Demo of attribute+Formula (TypeFormula — 셀별 enum 항목 적용)](https://jsfiddle.net/gh/get/library/pure/ibsheet/ibsheet8-manual-sample/tree/master/samples/properties/Col/attributeFormula-TypeChange-Enum/)
- [Demo of attribute+Formula (TypeFormula — 셀별 날짜 적용)](https://jsfiddle.net/gh/get/library/pure/ibsheet/ibsheet8-manual-sample/tree/master/samples/properties/Col/attributeFormula-TypeChange-Date/)
- [Demo of attribute+Formula (TypeFormula — 셀별 체크박스를 텍스트로 변환)](https://jsfiddle.net/gh/get/library/pure/ibsheet/ibsheet8-manual-sample/tree/master/samples/properties/Col/attributeFormula-BoolToText/)

### Read More
- [CanFormula row](/docs/props/row/can-formula)
- [CalcOrder row](/docs/props/row/calc-order)
- [attribute+Formula row](/docs/props/row/attribute-formula)
- [Formula col](/docs/props/col/formula)
- [calculate method](/docs/funcs/core/calculate)
- [recalculate method](/docs/funcs/core/recalculate)
- [recalculateRows method](/docs/funcs/core/recalculate-rows)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
