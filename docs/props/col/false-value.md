# FalseValue ***(col)***

<!-- synonyms: Bool 거짓 값, Bool 0 값, 체크해제 값, Y/N 매핑, false 매핑, server bool value -->

> `Bool` 타입 열에서 `0(false)` 상태에 해당하는 서버 측 데이터값을 설정합니다.  
> 데이터베이스 값이 `0` 외 다른 값(예: `"N"`)인 경우에 사용하며, 조회([doSearch](/docs/funcs/core/do-search) / [loadSearchData](/docs/funcs/core/load-search-data))와 저장([doSave](/docs/funcs/core/do-save) / [getSaveJson](/docs/funcs/core/get-save-json)) 시 변환됩니다.  
> 시트 내부 처리는 항상 `0(false)`로 다뤄지므로 [getValue](/docs/funcs/core/get-value) 등은 `0(false)`를 반환합니다.

### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`string` | 체크해제(`0`/`false`) 상태일 때 서버와 주고받을 값|

### Example
```javascript
// Bool 컬럼이지만 서버와는 "Y"/"N"으로 주고받음
options.Cols = [
    {
        Type: "Bool",
        Name: "ConfirmYN",
        Align: "Center",
        Width: 70,
        TrueValue: "Y",   // 화면 체크(1) ↔ 서버 "Y"
        FalseValue: "N"   // 화면 체크해제(0) ↔ 서버 "N"
    }
];
```

### Read More
- [TrueValue col](./true-value)
- [BoolFormatFix cfg](/docs/props/cfg/bool-format-fix)
- [Type appendix](/docs/appx/type)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
