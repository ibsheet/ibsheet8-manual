# Enum ***(col)***

<!-- synonyms: 드랍리스트 항목, 콤보박스 아이템, 라디오 항목, 표시 항목, 선택지, dropdown items, radio items -->

> [Type](/docs/appx/type)이 `Enum`이나 `Radio`인 컬럼에서 화면에 보여질 항목 목록을 설정합니다.  
> **문자열의 첫 글자를 구분자**로 사용하여 항목들을 이어 붙인 형식입니다. (예: `"|A|B|C"`, `"#A#B#C"` 모두 동일)  
> 실제 데이터값은 [EnumKeys](./enum-keys)로 별도 지정합니다. 미설정 시 `Enum`에 적힌 항목명이 그대로 데이터값이 됩니다.  
> `Radio` 타입에서는 라디오 버튼 옆에 표시될 텍스트를 정의하므로 사실상 필수입니다.

###
![Enum타입](/assets/imgs/enum1.png "Enum")<br/>[그림1] Enum<br/>
![Radio타입](/assets/imgs/radioEnum.png "Radio")<br/>[그림2] Radio


### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`string` | 첫 글자를 구분자로 하는 항목 문자열 (예: `"#사장#부사장#전무#상무#이사"`)|


### Example
```javascript
options.Cols = [
    // 구분자만 다르고 동일한 결과 (둘 다 4개 항목)
    {Type: "Enum", Name: "relation", Enum: "|직계존속|직계비속|배우자|자녀"},
    {Type: "Enum", Name: "relation", Enum: "#직계존속#직계비속#배우자#자녀"},

    // Radio 타입: Enum으로 라디오 옆 텍스트, EnumKeys로 실제 저장값 매핑
    {Type: "Radio", Name: "rate", Enum: "|상|중|하", EnumKeys: "|H|M|L"}
];
```

### Read More
- [EnumKeys col](./enum-keys)
- [EnumFilter col](./enum-filter)
- [IconAlign col](./icon-align)
- [MenuHSeparator cfg](/docs/props/cfg/menu-h-separator)
- [Range col](./range)
- [Related col](./related)
- [ShowImage cfg](/docs/props/cfg/showImage)
- [Type appendix](/docs/appx/type)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
