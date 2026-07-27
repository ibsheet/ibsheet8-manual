# Popup 타입 마이그레이션

ibsheet7의 `Popup` 타입은 ibsheet8에는 별도 타입으로 존재하지 않습니다. 셀 우측에 버튼을 두고 클릭하면 사용자가 정의한 팝업을 띄우는 형태로 구현합니다.

#### 1) 단순 형태 — `Button` 속성 직접 사용
열 우측에 항상 버튼을 표시하려면 [Button (col)](/docs/props/col/button) 속성에 이미지 경로를 설정합니다.

```javascript
//AS-IS
{Header:"부서", Type:"Popup", SaveName:"DEPTPOP"}
```

```javascript
//TO-BE
{Header:"부서", Type:"Text", Name:"DEPTPOP", Button:"../assets/imgs/popup.png"}
```

버튼 클릭 시 발생하는 이벤트는 [onButtonClick (event)](/docs/events/on-button-click)에서 처리합니다.

#### 2) ibsheet7 Popup 모양 그대로 — `IB_Preset.Popup` Extend
`IBSheet-common.js` 파일에 `IB_Preset.Popup`을 [Extend](/docs/props/col/extend)하면 ibsheet7의 Popup 컬럼 모양을 그대로 재현할 수 있습니다.

`IB_Preset.Popup`은 `ButtonFormula`로 **편집 가능한 셀에서만 버튼을 표시**하고, (1)의 `Button` 속성은 편집 가능 여부와 무관하게 항상 버튼이 표시됩니다.

```javascript
var initSheet = {
    // IB_Preset.Popup은 내부적으로 ButtonFormula(attribute+Formula)를 사용하므로 CanFormula·CalcOrder 필수
    Def: {
        Row: { CanFormula: 1, CalcOrder: "DEPTPOPButton" }
    },
    Cols:[
        //ibsheet7 Popup 열처럼 동작하는 열을 만든다.
        {
            Header: "부서",
            Name: "DEPTPOP",
            Extend: IB_Preset.Popup
        }
    ],
    Events: {
        // ibsheet7 Popup 타입처럼 셀 텍스트 직접 편집은 막고 버튼 클릭만 허용
        onStartEdit: function(paramObject) {
            if (paramObject.col === "DEPTPOP") return true;  // 편집 시작 취소
        }
    }
};
```

여러 Popup 컬럼이 있는 경우, 컬럼에 `Popup:1` 같은 사용자 정의 속성을 두고 `onStartEdit`에서 한 번에 분기 처리합니다.  
이렇게 하면 컬럼이 늘어나도 이벤트 코드는 그대로 유지됩니다.

```javascript
var initSheet = {
    Def: {
        Row: { CanFormula: 1, CalcOrder: "DEPTPOPButton,EMPPOPButton" }
    },
    Cols:[
        {Header:"부서", Name:"DEPTPOP", Extend: IB_Preset.Popup, Popup:1},
        {Header:"사원", Name:"EMPPOP",  Extend: IB_Preset.Popup, Popup:1}
    ],
    Events: {
        onStartEdit: function(evtParam) {
            // 컬럼 정의에 Popup:1로 표시된 컬럼은 모두 편집 시작 취소
            if (evtParam.sheet.Cols[evtParam.col].Popup === 1) return true;
        }
    }
};
```

참고
- `IB_Preset.Popup`의 내용을 ibsheet-common.js에서 찾아보면 [ButtonFormula](/docs/props/col/attribute-formula)([attribute+Formula (col)](/docs/props/col/attribute-formula))를 사용하므로, [Def/Row](/docs/start/init-structure)에 [CanFormula (row)](/docs/props/row/can-formula) 속성을 `1`로 설정하고 [CalcOrder (row)](/docs/props/row/calc-order)에 `열이름Button` 형식 항목을 추가해야 합니다.
- 여러 컬럼에 적용할 경우 CalcOrder를 `"DEPTPOPButton,EMPPOPButton"` 형식으로 콤마로 연결합니다(항목 사이 공백 없음).
- ibsheet7의 `Popup` 타입은 기본적으로 셀 텍스트 편집이 불가했지만, `IB_Preset.Popup`은 `Type:"Text"` 기반이므로 ibsheet8에서는 셀이 기본 편집 가능합니다. ibsheet7과 동일하게 셀 텍스트 편집을 막으려면 [onStartEdit (event)](/docs/events/on-start-edit)에서 `return true`로 편집 시작을 취소합니다. `CanEdit:0`은 사용하지 마세요 — `ButtonFormula`가 `getCanEdit` 기반이라 버튼도 함께 숨겨집니다.
- 버튼 클릭 이벤트는 [onButtonClick (event)](/docs/events/on-button-click)에서 처리합니다.
