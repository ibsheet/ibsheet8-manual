# BoolFormatFix ***(cfg)***

<!-- synonyms: Bool 저장 형식, Bool 문자열 변환, Bool 타입 저장, getSaveJson Bool, Bool 1/0 문자열 -->

> 저장 함수([getSaveJson](/docs/funcs/core/get-save-json), [getSaveString](/docs/funcs/core/get-save-string), [doSave](/docs/funcs/core/do-save)) 호출 시 `Type:"Bool"` 컬럼 값을 숫자 대신 문자열로 추출할지 여부를 설정합니다.  
> 컬럼 단위 [FormatFix](/docs/props/col/format-fix)와 함께 설정된 경우 이 설정이 우선 적용됩니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)` | Bool 컬럼 값을 숫자 `1`/`0`으로 출력 (`default`)|
|`1(true)` | Bool 컬럼 값을 문자열 `"1"`/`"0"`으로 출력|

### Example
```javascript
options.Cfg = {
    BoolFormatFix: 1
};
options.Cols = [
    {Type: "Bool", Name: "CheckData"}
];

sheet.getSaveJson();
// BoolFormatFix:0 (기본): { "CheckData": 1   }
// BoolFormatFix:1:       { "CheckData": "1" }
```

### Read More
- [FormatFix col](/docs/props/col/format-fix)
- [getString method](/docs/funcs/core/get-string)
- [getSaveJson method](/docs/funcs/core/get-save-json)
- [getSaveString method](/docs/funcs/core/get-save-string)

### Since

|product|version|desc|
|---|---|---|
|core|8.3.0.61|기능 추가|
