# EnumExpand ***(col)***

<!-- synonyms: Enum 방향, Enum 펼침 방향, 드롭다운 방향, 위아래 방향, Enum 강제 방향, dropdown direction, enum vertical align, EnumVAlign -->

> [Type](/docs/appx/type)이 `Enum`인 열에서 편집 시 드롭다운 메뉴가 펼쳐지는 위/아래 방향을 강제로 지정합니다.  
> 기본 동작은 셀의 화면상 위치와 남은 공간을 고려해 위 또는 아래로 자동 결정되지만, 이 옵션을 지정하면 남은 공간에 관계없이 지정한 방향으로 고정됩니다.  

### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`"Down"`|Enum 메뉴가 항상 셀 아래쪽으로 펼쳐지도록 강제|
|`"Up"`|Enum 메뉴가 항상 셀 위쪽으로 펼쳐지도록 강제|

### Example
```javascript
options.Cols = [
    // 상단에 배치되는 열 — 항상 아래로 펼침
    {Type: "Enum", Name: "Status", Enum: "|A|B|C", EnumExpand: "Down"},

    // 하단에 배치되는 열 — 항상 위로 펼침
    {Type: "Enum", Name: "Category", Enum: "|X|Y|Z", EnumExpand: "Up"}
];
```

### Read More
- [Type appendix](/docs/appx/type)
- [Enum col](./enum)
- [EnumMenu col](./enum-menu)
- [MenuMaxHeight cfg](/docs/props/cfg/menu-max-height)

### Since

|product|version|desc|
|---|---|---|
|core|8.4.0.11|기능 추가|
