# EnumKeys ***(col)***

<!-- synonyms: 항목 실제값, Enum 값 매핑, 콤보박스 저장값, 라디오 저장값, 표시값 실제값 분리, Enum key -->

> [Enum](./enum)으로 설정한 화면 표시 항목과 1:1 매핑되는 **실제 데이터값**을 설정합니다.  
> 첫 글자를 구분자로 하여 값들을 이어 붙인 문자열 형식입니다.  
> 이 속성을 설정하면 조회/저장 시 화면 표시값(`Enum`) 대신 `EnumKeys` 값이 사용됩니다.

### 주의 사항
- `EnumKeys`의 각 값은 **유일**해야 합니다. 동일한 값을 중복해서 사용하면 안 됩니다.
- [Type](/docs/appx/type)이 `Radio`인 컬럼은 [Enum](./enum)과 `EnumKeys`의 **항목 개수를 동일하게** 설정해야 체크 동작이 정상적으로 이루어집니다.

### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`string` | 첫 글자를 구분자로 하는 값 문자열 (예: `"#01#02#03#04"`)|

### Example
```javascript
options.Cols = [
    // 화면에는 "직계존속/직계비속/배우자/자녀", 데이터값은 "A0/A1/B0/C0"
    {Type: "Enum", Name: "relation",
        Enum:     "|직계존속|직계비속|배우자|자녀",
        EnumKeys: "|A0|A1|B0|C0"},

    // Radio: Enum과 EnumKeys의 항목 개수가 동일해야 함 (3:3)
    {Type: "Radio", Name: "rate",
        Enum:     "|상|중|하",
        EnumKeys: "|H|M|L"}
];
```

### Read More
- [Enum col](./enum)
- [EnumFilter col](./enum-filter)
- [MenuHSeparator cfg](/docs/props/cfg/menu-h-separator)
- [Related col](./related)
- [Type appendix](/docs/appx/type)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
