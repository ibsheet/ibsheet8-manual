# Uncheck ***(cell)***

<!-- synonyms: 체크해제 허용, 라디오 체크해제, 그룹 체크해제, bool 토글, uncheck cell -->

> `Type:"Bool"` 셀에서 [Radio](/docs/props/cell/radio)나 [BoolGroup](/docs/props/cell/bool-group)으로 단일 선택을 적용한 경우, 이미 체크된 셀을 다시 클릭했을 때 체크해제를 허용할지 여부를 설정합니다.

###
![Radio](/assets/imgs/radio.png "같은 행에서 하나만 선택 가능")

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)` | 체크해제 허용 안 함|
|`1(true)` | 체크해제 허용 (`default`)|

### Example
```javascript
// AR99의 CLS 셀에 체크해제 비허용
sheet.setAttribute(sheet.getRowById("AR99"), "CLS", "Uncheck", 0);
```

### Read More
- [Uncheck col](/docs/props/col/uncheck)
- [Radio cell](/docs/props/cell/radio)
- [BoolGroup cell](/docs/props/cell/bool-group)
- [RadioUncheck cell](/docs/props/cell/radio-uncheck)
- [Type appendix](/docs/appx/type)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
