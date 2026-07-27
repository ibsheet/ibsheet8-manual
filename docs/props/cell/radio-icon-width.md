# RadioIconWidth ***(cell)***

<!-- synonyms: 라디오 아이콘 너비, 라디오 이미지 너비, radio icon width cell, custom radio width -->

> [RadioIcon](/docs/props/cell/radio-icon) 속성으로 라디오 아이콘을 커스텀 이미지로 설정한 경우, 이미지의 너비를 픽셀 단위로 설정합니다.

### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`number`|라디오 아이콘 이미지의 너비 (px)|

### Example
```javascript
// 22px 너비의 커스텀 라디오 아이콘을 특정 셀에 적용
var row = sheet.getRowById("AR99");
sheet.setAttribute(row, "CLS", "RadioIcon", "|Off.gif|On.gif");
sheet.setAttribute(row, "CLS", "RadioIconWidth", 22);
```

### Read More
- [RadioIcon cell](/docs/props/cell/radio-icon)
- [Radio cell](/docs/props/cell/radio)
- [RadioUncheck cell](/docs/props/cell/radio-uncheck)
- [RadioIconWidth col](/docs/props/col/radion-icon-width)
- [Type appendix](/docs/appx/type)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
