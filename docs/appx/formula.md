# Formula ***(appendix)***

<!-- synonyms: 수식, 계산식, formula, 셀 계산, 자동 계산, 트리 합계 -->

> 셀의 값(value) 또는 속성(글자색, 배경색 등)을 다른 열의 값과의 계산을 통해 자동으로 설정하는 기능입니다.

### Formula 종류
1. **일반 Formula** — 셀의 값을 계산식으로 설정
2. **속성 Formula** — 셀/열/행의 속성(Color, TextColor, CanEdit 등)을 계산식으로 설정

### 동작 규칙
> Formula로 계산된 셀은 기본적으로 편집 불가능하며, `CanEditFormula`를 `1`로 설정해야 편집 가능합니다.  
> Formula 함수는 인자(`fr`)를 받아 `fr.Sheet`, `fr.Row`, `fr.Col`로 시트/행/현재 컬럼명에 접근합니다.  
> 문자열 형식 Formula에서는 컬럼명을 식에 그대로 사용하며, 예약어 `Sheet`, `Row`, `Col`로 접근합니다.  
> 외부 함수를 단독 사용 시 함수는 반드시 값을 `return`해야 적용됩니다.  
> Formula로 값이 변경되면 별도 refresh 없이 화면에 즉시 반영됩니다.

### 필수 설정
- Formula 사용 시 [CanFormula (row)](/docs/props/row/can-formula)를 `1`로 설정해야 합니다.
- 속성 Formula(attribute+Formula) 사용 시 [CalcOrder (row)](/docs/props/row/calc-order)를 반드시 함께 정의해야 합니다.
- 속성 Formula와 일반 Formula를 함께 쓰는 경우, 일반 Formula의 컬럼명도 `CalcOrder`에 포함해야 합니다.

### Syntax
```javascript
options.Def = {
    Row: {
        CanFormula: 1,                  // Formula 동작 활성화
        CalcOrder: "Formula가 선언된 열이름들을 ',' 로 연결"
    }
};
options.Cols = [
    {
        Name: "...",
        // 일반 Formula — 셀 값 계산
        Formula: "주변 열과의 계산식 또는 함수 참조",

        // 속성 Formula — 속성 값 계산 (Color, TextColor, CanEdit 등)
        속성명Formula: "속성 값을 설정하기 위한 계산식"
    }
];
```

### Formula 적용 대상
| 대상 | 설명 |
|---|---|
| 셀 값 | 셀에 들어갈 값을 동적으로 계산 |
| 셀 속성 | 특정 셀의 속성 값을 동적으로 계산 |
| 열 속성 | 특정 열 전체의 속성 값을 동적으로 계산 |

### Example
```javascript
options.Def = {
    Row: {
        CanFormula: 1,
        // CalcOrder 사이에는 띄어쓰기를 넣지 말 것
        CalcOrder: "sCountColor,sMoneyTextColor,sResult,sComment,sGrade"
    }
};

options.Cols = [
    {
        Name: "sCount", Type: "Int",
        // 배경색을 값에 따라 동적으로 설정 (속성 Formula)
        ColorFormula: 'Value < 0 ? "rgb(245, 226, 24)" : Value == 0 ? "" : "rgb(11, 231, 109)"'
    },
    {
        Name: "sMoney", Type: "Int",
        // 텍스트 컬러 속성 (속성 Formula)
        TextColorFormula: "Value < 3000 ? '#ff0000' : '#f0694e'"
    },
    {
        Name: "sResult", Type: "Float",
        // 값 계산 (string 형식 일반 Formula)
        Formula: "sCount * sPrice - (sCount * sPrice * sDiscount) / 100"
    },
    {
        Name: "sComment", Type: "Text",
        // 외부 함수 호출 (string 형식)
        Formula: "useFormula1(Sheet,Row,Col)"
    },
    {
        Name: "sGrade", Type: "Text",
        // 외부 함수 참조 (function 형식)
        Formula: useFormula2
    }
];

function useFormula1(fr) {
    // fr.Sheet, fr.Row, fr.Col 로 접근
    var rtnValue = (fr.Row['QT1'] + fr.Row['QT2']) / 2;
    return rtnValue;  // 반드시 return 필요
}

function useFormula2(obj) {
    var Value = obj.Row[obj.Col];
    return Value;
}
```

### Tree 구조에서의 활용 패턴

트리 시트에서 부모/자식 관계를 활용해 Formula를 작성할 수 있습니다. `fr.Row`의 트리 노드 속성으로 부모/자식 행에 접근합니다.

| 속성 | 설명 |
|---|---|
| `fr.Row.childNodes.length` | 자식 수 — `0`이면 leaf, `> 0`이면 부모 |
| `fr.Row.firstChild`, `nextSibling` | 직계 자식 순회 |
| `fr.Row.parentNode` | 부모 행 |
| `fr.Row.Level` | 트리 레벨 (`0`=루트) |
| `r.Deleted` | 삭제 상태(`1`) — 합계에서 제외 시 활용 |

**자식 합계 (삭제행 제외)**
```javascript
function TreeSumExFormula(fr) {
    if (fr.Row.childNodes.length) {
        // 부모 행: 직계 자식의 합 (삭제 제외)
        var sum = 0;
        for (var r = fr.Row.firstChild; r; r = r.nextSibling) {
            if (!r.Deleted) sum += (r[fr.Col] || 0);
        }
        return sum;
    } else {
        // leaf 행: 본인 값 + 편집 가능 설정
        fr.Row[fr.Col + "CanEdit"] = 1;
        return fr.Row[fr.Col];
    }
}
```

**부모 행에서 자식 건수 표시**
```javascript
function ChildCountFormula(fr) {
    if (fr.Row.Level === 0) {
        // 루트(부모) 행: 자식 건수 "N건" 표시
        var count = 0;
        for (var r = fr.Row.firstChild; r; r = r.nextSibling) {
            if (!r.Deleted) count++;
        }
        return count + "건";
    } else {
        // 하위 행: 본인 값
        fr.Row[fr.Col + "CanEdit"] = 1;
        return fr.Row[fr.Col];
    }
}
```

**leaf 행만 편집 가능하게 만들기**

위 예제에서 `fr.Row[fr.Col + "CanEdit"] = 1` 은 행+컬럼 단위로 편집 허용을 선언하는 패턴입니다. Formula 함수가 leaf에 도달했을 때만 이 줄이 실행되므로 부모 행은 자동으로 읽기 전용이 됩니다.

### Read More
- [Formula col](/docs/props/col/formula)
- [CanFormula row](/docs/props/row/can-formula)
- [CalcOrder row](/docs/props/row/calc-order)
- [attribute+Formula col](/docs/props/col/attribute-formula)
- [attribute+Formula row](/docs/props/row/attribute-formula)
- [attribute+Formula cell](/docs/props/cell/attribute-formula)
- [FormulaRow col](/docs/props/col/formula-row)
- [calculate method](/docs/funcs/core/calculate)
- [addFormula method](/docs/funcs/core/add-formula)

### Since

| product | version | desc |
|---|---|---|
| core | 8.0.0.0 | 기능 추가 |
