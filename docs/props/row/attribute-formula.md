# attribute+Formula ***(row)***

<!-- synonyms: 행 속성 수식, row attribute formula, 행 속성 자동 계산, 행 색상 수식, 편집 가능 수식 -->

> 행별로 배경색(`Color`), 편집 가능 여부(`CanEdit`), 텍스트 색(`TextColor`) 등의 속성을 조건에 따라 다르게 적용할 때 이용합니다.  
> [CanFormula](/docs/props/row/can-formula)가 `1`로 설정되어야 동작하며, [CalcOrder](/docs/props/row/calc-order)에 속성명을 반드시 정의해야 합니다.  
> 도움말 [properties → Row](/docs/props/row/) 카테고리에 정의된 속성만 `속성명Formula` 형식으로 사용할 수 있습니다.

### Type
`mixed`( `function` \| `string` )

### Options
|Value|Description|
|-----|-----|
|`string`|컬럼명을 식에 직접 사용한 수식 문자열 (예: `"Amount > 500 ? '#FFFFDD' : ''"`)|
|`function`|계산 결과를 `return`하는 함수 (return 값이 없으면 반영 안 됨)<br/>첫 번째 인자로 `fr` 객체가 자동 전달됨|

### Parameters

**function 형식** — 함수 인자 `fr`의 속성

|Name|Type|Description|
|---|---|---|
|`Sheet`|`object`|시트 객체|
|`Row`|`object`|Formula가 적용된 행 객체|
|`Attr`|`string`|Formula가 적용되는 속성명 (예: `Color`, `CanEdit`)|

**string 형식** — 식 내 예약어

|Name|Type|Description|
|---|---|---|
|`Sheet`|`object`|시트 객체|
|`Row`|`object`|Formula가 적용된 행 객체|
|`Attr`|`string`|Formula가 적용되는 속성명 (예: `Color`, `CanEdit`)|
|컬럼명|`mixed`|컬럼명을 직접 사용 시 해당 셀의 값 (예: `Amount > 500`)|

### 주의 사항
> - [CanFormula](/docs/props/row/can-formula)를 설정하지 않으면 Formula가 동작하지 않습니다.
> - 속성(attribute+Formula)는 [CalcOrder](/docs/props/row/calc-order)가 항상 필요합니다.
> - [CalcOrder](/docs/props/row/calc-order)는 속성명만 적습니다. [attribute+Formula (col)](/docs/props/col/attribute-formula)과 달리 열이름이 붙지 않습니다. 예: `"Color,CanEdit"`
> - [CalcOrder](/docs/props/row/calc-order) 항목 사이에 공백이 들어가면 인식되지 않습니다. `"Color, CanEdit"`가 아니라 `"Color,CanEdit"`.

### Example
```javascript
options.Def.Row = {
    CanFormula: 1,
    CalcOrder: "Color,CanEdit",   // 속성명 사이에 공백 없이

    // string 형식 — 컬럼명을 식에 직접 사용
    ColorFormula: "DeptCd == '1B' ? '#FFFFDD' : ''",

    // function 형식 — fr 인자로 행 데이터 접근
    CanEditFormula: function(fr) {
        if (fr.Row["FinishedYN"]) return 0;
    }
};

options.Cols = [
    {Header: "결산완료", Type: "Bool", Name: "FinishedYN"},
    {Header: "부서", Type: "Enum", Name: "DeptCd",
        Enum: "|총무|회계|인사|영업|개발",
        EnumKeys: "|2A|1B|C9|B4|D0"}
];
```

### Read More
- [CanFormula row](/docs/props/row/can-formula)
- [CalcOrder row](/docs/props/row/calc-order)
- [attribute+Formula col](/docs/props/col/attribute-formula)
- [Formula col](/docs/props/col/formula)
- [calculate method](/docs/funcs/core/calculate)
- [recalculate method](/docs/funcs/core/recalculate)
- [recalculateRows method](/docs/funcs/core/recalculate-rows)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
