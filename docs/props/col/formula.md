# Formula ***(col)***

<!-- synonyms: 컬럼 수식, formula col, 컬럼 자동 계산, 셀 값 수식, 엑셀 수식 -->

> 엑셀 수식과 유사한 기능입니다.  
> 컬럼에 수식을 설정하면 다른 셀 값이나 함수를 활용해 모든 행의 셀 값을 자동 계산합니다.  
> 조회 시, 관련 컬럼 값 편집 시, [calculate](/docs/funcs/core/calculate) 호출 시 재계산됩니다.  
> Formula를 설정한 컬럼은 자동으로 편집 불가 상태가 됩니다.  
> Formula 안에서 자기 자신의 컬럼 값을 참조하면 무한루프에 빠질 수 있으므로 권장하지 않습니다.  
> 셀 속성(편집 제어, 색상 등)을 수식으로 설정하려면 [attribute+Formula (col)](/docs/props/col/attribute-formula), [attribute+Formula (row)](/docs/props/row/attribute-formula)를 참고하세요.  
> [CanFormula](/docs/props/row/can-formula)가 `1`로 설정되어야 동작하며, 컬럼 간 의존 순서가 있거나 [attribute+Formula](/docs/props/col/attribute-formula)와 함께 사용할 때는 [CalcOrder](/docs/props/row/calc-order)를 정의해야 합니다.


### Type
`mixed`( `function` \| `string` )

### Options
|Value|Description|
|-----|-----|
|`string`|컬럼명을 그대로 식에 사용하는 수식 문자열 (예: `"qt1 + qt2 - discount * 0.1"`)|
|`function`|계산 결과를 `return`하는 함수 (return 값이 없으면 반영 안 됨)<br/>첫 번째 인자로 `fr` 객체가 자동 전달됨|

### Parameters

**function 형식** — 함수 인자 `fr`의 속성

|Name|Type|Description|
|---|---|---|
|`Sheet`|`object`|시트 객체|
|`Row`|`object`|행 객체|
|`Col`|`string`|Formula 설정한 컬럼명|

**string 형식** — 식 내 예약어

|Name|Type|Description|
|---|---|---|
|`Sheet`|`object`|시트 객체|
|`Row`|`object`|행 객체|
|`Col`|`string`|Formula 설정한 컬럼명|
|`Value`|`mixed`|Formula 설정한 컬럼의 셀 값|
|컬럼명|`mixed`|컬럼명을 직접 사용 시 해당 셀의 값 (예: `qt1 + qt2`)|

> 외부 함수 호출 (function 형식): `Formula: 함수명` (첫 번째 인자로 `fr` 객체 자동 전달).  
> 외부 함수 호출 (string 형식): `Formula: "함수명(Sheet, Row, Col, Value)"`처럼 사용자가 호출 식을 직접 작성 (괄호 안 인자는 예약어, 컬럼명에서 자유롭게 선택).

### 주의 사항
> - [CanFormula](/docs/props/row/can-formula)를 설정하지 않으면 Formula가 동작하지 않습니다.
> - 컬럼 간 의존 순서가 있거나 [attribute+Formula](/docs/props/col/attribute-formula)와 함께 사용할 때 [CalcOrder](/docs/props/row/calc-order)가 없으면 동작하지 않거나 잘못된 값이 반환될 수 있습니다.
> - [CalcOrder](/docs/props/row/calc-order) 항목 사이에 공백이 들어가면 인식되지 않습니다. `"a, b, c"`가 아니라 `"a,b,c"`.
> - `IB_Preset.TreeSumFormula` 등 [ibsheet-common.js](https://www.ibsheet.com/v8/assets/lib/ibsheet/plugins/ibsheet-common.js)가 제공하는 함수도 Formula 기능이므로 [CanFormula](/docs/props/row/can-formula)와 [CalcOrder](/docs/props/row/calc-order)가 동일하게 필요합니다.
> - 조회 데이터에 빈 문자열(`""`), `null`, `undefined`가 섞여 있는 경우 `function` 형식 Formula는 `NaN`이나 문자열 결합이 발생할 수 있습니다.

### Example
```javascript
options.Def.Row = {CanFormula: 1, CalcOrder: "yearSum,total,result"};
options.Cols = [
    {Type: "Int",   Name: "qt1"},
    {Type: "Int",   Name: "qt2"},

    // string 형식 — 식에 컬럼명을 그대로 사용
    {Type: "Int",   Name: "yearSum", Formula: "qt1 + qt2"},

    {Type: "Float", Name: "rate"},

    // function 형식 — fr 인자로 행/시트 정보 접근
    {Type: "Float", Name: "total",
        Formula: function(fr) {
            return fr.Row["yearSum"] * fr.Row["rate"];
        }
    },

    // Type에 맞는 값을 return — 여기서는 Text Type이므로 문자열 반환
    {Type: "Text", Name: "result",
        Formula: function(fr) {
            return fr.Row["total"] >= 100 ? "달성" : "미달";
        }
    }
];

// X — 자기 자신을 참조하면 무한루프
{Type: "Int", Name: "yearSum",
    Formula: function(fr) {
        return fr.Row["yearSum"] + fr.Row["qt2"]; // yearSum이 바뀌면 다시 Formula 실행 → 무한루프
    }
}
```

#### Tree Example

트리 구조 시트에서는 `ibsheet-common.js`가 제공하는 `IB_Preset.*Formula` 프리셋(`TreeSumFormula`, `TreeAvgFormula`, `TreeCountFormula`, `TreeMaxFormula`, `TreeMinFormula`)이나 커스텀 함수로 부모 행에 자식 행 집계 결과를 표시할 수 있습니다.  
`IB_Preset.*Formula`도 Formula 기능이므로 `Def.Row.CanFormula:1` 설정이 동일하게 필요하며, 트리 시트로 동작하려면 `Cfg.MainCol` 설정도 필요합니다 (Read More 참고).

```javascript
{Header:"합계", Type:"Int", Name:"sum", Formula: IB_Preset.TreeSumFormula}
```

상태가 삭제(`Row.Deleted`)인 행을 제외하고 자식 행 합계를 계산해야 할 때는 커스텀 함수로 처리합니다.  
트리의 leaf 행(자식이 없는 말단 행)은 사용자가 직접 값을 입력해야 하므로 자기 자신의 `CanEdit`을 켜줍니다.

```javascript
{Type: "Int", Name: "sumEx",
    Formula: function(fr) {
        if (fr.Row.childNodes.length) {                              // 자식이 있으면 부모 행
            var sum = 0;
            for (var r = fr.Row.firstChild; r; r = r.nextSibling) {  // 직계 자식 순회
                if (!r.Deleted) sum += (r[fr.Col] || 0);             // 삭제 상태인 행 제외
            }
            return sum;
        } else {                                                      // leaf 행
            fr.Row[fr.Col + "CanEdit"] = 1;
            return fr.Row[fr.Col];
        }
    }
}

// 더 다양한 패턴은 아래 Try it 데모 참고
```

![Tree Formula 동작 — 부서별 실적 집계](/assets/imgs/formula_tree.png)

### Try it
- [Demo of Formula](https://jsfiddle.net/gh/get/library/pure/ibsheet/ibsheet8-manual-sample/tree/master/samples/properties/Col/Formula/)
- [Demo of Tree Formula (부서별 실적 집계)](https://jsfiddle.net/gh/get/library/pure/ibsheet/ibsheet8-manual-sample/tree/master/samples/properties/Col/Formula-TreeSum/)

### Read More
- [CanFormula row](/docs/props/row/can-formula)
- [CalcOrder row](/docs/props/row/calc-order)
- [attribute+Formula col](/docs/props/col/attribute-formula)
- [attribute+Formula row](/docs/props/row/attribute-formula)
- [MainCol cfg](/docs/props/cfg/main-col)
- [calculate method](/docs/funcs/core/calculate)
- [recalculate method](/docs/funcs/core/recalculate)
- [recalculateRows method](/docs/funcs/core/recalculate-rows)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
