# RadioIconWidth ***(col)***

<!-- synonyms: 라디오 아이콘 너비, 라디오 이미지 너비, radio icon width, custom radio width -->

> [RadioIcon](./radio-icon) 속성으로 라디오 아이콘을 커스텀 이미지로 설정한 경우, 이미지의 너비를 픽셀 단위로 설정합니다.

### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`number`|라디오 아이콘 이미지의 너비 (px)|

### Example
```javascript
options.Cols = [
    // 22px 너비의 커스텀 라디오 아이콘 사용
    {Type: "Radio", Name: "st1", RadioIcon: "|Off.gif|On.gif", RadioIconWidth: 22}
];
```

### Read More
- [RadioIcon col](./radio-icon)
- [Radio col](./radio)
- [RadioUncheck col](./radio-uncheck)
- [RadioIconWidth cell](/docs/props/cell/radio-icon-width)
- [Type appendix](/docs/appx/type)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
