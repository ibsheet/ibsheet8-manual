# RangeEnumIconLeft ***(cfg)***

<!-- synonyms: Enum 체크박스 위치, Range 체크박스 왼쪽, 드랍리스트 체크 위치 -->

> `Enum` 타입에 [Range](/docs/props/col/range)`:1` 사용 시 드랍리스트 항목 옆에 표시되는 체크박스의 위치(좌/우)를 설정합니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)` | 체크박스를 항목 오른쪽에 표시 (`default`)|
|`1(true)` | 체크박스를 항목 왼쪽에 표시|

### Example
```javascript
options = {
    Cfg: {
        RangeEnumIconLeft: true   // 드랍리스트 항목 왼쪽에 체크박스 표시
    },
    Cols: [
        // Enum + Range:1 컬럼이 있어야 효과 확인 가능
        {Header: "명절선물", Type: "Enum", Name: "gift", Range: 1,
            Enum:     "|갈비세트|조기세트|사과배|스팸3호",
            EnumKeys: "|A|B|C|D"}
    ]
};
```

### Read More
- [Enum col](/docs/props/col/enum)
- [FilterEnumIconLeft cfg](./filter-enum-icon-left)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.8|기능 추가|
