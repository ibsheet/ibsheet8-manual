# Combo/ComboEdit 타입 마이그레이션

<!-- synonyms: IBSheet7, 마이그레이션, sheet7, migration, v7, v8, ibsheet7에서 ibsheet8로, Combo, ComboEdit, Combo 타입, ComboEdit 타입, 콤보 박스, dropdown, combobox, Enum 변환 -->

`Combo` 타입은 [Enum](/docs/appx/type)타입으로 변경되었고, `ComboText`, `ComboCode`는 각각 [Enum (col)](/docs/props/col/enum), [EnumKeys (col)](/docs/props/col/enum-keys) 속성으로 변경되었습니다.

```javascript
//AS-IS
{Header:"직급", Type:"Combo", SaveName:"Position", ComboText:"사원|대리|과장|차장|부장", ComboCode:"A0|A1|B0|B1|B3"}
```
```javascript
//TO-BE (Enum,EnumKeys속성의 첫번째 글자가 구분자로 사용됨을 주의)
{Header:"직급", Type:"Enum", Name:"Position", Enum:"|사원|대리|과장|차장|부장", EnumKeys:"|A0|A1|B0|B1|B3"}
```

항목이 많아 검색이 필요한 경우 [EnumFilter (col)](/docs/props/col/enum-filter):`1`을 추가하면 드롭다운에 검색 input이 표시됩니다 (`core 8.3.0.48+`).

```javascript
{Header:"직급", Type:"Enum", Name:"Position",
 Enum:"|사원|대리|과장|차장|부장", EnumKeys:"|A0|A1|B0|B1|B3",
 EnumFilter: 1}
```

> 사용자가 새 값을 직접 입력할 필요 없이 정의된 항목 중에서만 선택하면 되는 경우, 위 Combo 변환에 `EnumFilter:1`을 추가하는 게 더 단순합니다. 새 값을 직접 입력해야 하는 경우에만 아래 `ComboEdit` 패턴을 사용하세요.

`ComboEdit`는 [Defaults (col)](/docs/props/col/defaults), [Format (col)](/docs/props/col/format), [EditFormat (col)](/docs/props/col/edit-format), [Suggest (col)](/docs/props/col/suggest) 속성을 사용하여 유사하게 동작하는 열을 만드실 수 있습니다.
```javascript
//AS-IS
{Header:"직급", Type:"ComboEdit", SaveName:"Position", ComboText:"사원|대리|과장|차장|부장|이사|상무|사장", ComboCode:"A0|A1|B0|B1|B3|C0|C1|C2"}
```

```javascript
//TO-BE
var comboText = "사원|대리|과장|차장|부장|이사|상무|사장";
var comboCode = "A0|A1|B0|B1|B3|C0|C1|C2";

{
    Header:"직급", Type:"Text", Name:"Position",
    Button: "Defaults",
    // 화면에 표시될 셀 값의 Format 형태를 설정. 값이 A0면 "사원"이 화면에 표시
    Format: {
        "A0": "사원",
        "A1": "대리",
        "B0": "과장",
        "B1": "차장",
        "B3": "부장",
        "C0": "이사",
        "C1": "상무",
        "C2": "사장"
    },
    // 셀 편집시 화면에 표시될 Format 형태를 설정
    EditFormat: {
        "A0": "사원",
        "A1": "대리",
        "B0": "과장",
        "B1": "차장",
        "B3": "부장",
        "C0": "이사",
        "C1": "상무",
        "C2": "사장"
    },
    Suggest:"|"+comboText,  // 입력시 아이템 필터링
    Defaults: "|"+comboCode // 셀 선택시 기본값
}
```
위와 같이 설정하면 사용가능합니다. `ComboEdit` 사용은 [onBeforeCreate (static)](/docs/static/on-before-create)이벤트에서 공통으로 설정하여 사용하시기 바랍니다.
