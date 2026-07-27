# RadioUncheck ***(cell)***

<!-- synonyms: 라디오 체크해제, 라디오 선택 취소, 라디오 토글, radio uncheck cell, 같은 라디오 다시 클릭 -->

> `Type:"Radio"`인 셀에서 이미 선택된 항목을 다시 클릭했을 때 체크해제를 허용할지 여부를 설정합니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)` | 체크해제 허용 안 함 (`default`)|
|`1(true)` | 체크해제 허용|

### Example
```javascript
// AR99의 CLS 셀에 체크해제 허용
sheet.setAttribute(sheet.getRowById("AR99"), "CLS", "RadioUncheck", 1);
```

### Read More
- [RadioUncheck col](/docs/props/col/radio-uncheck)
- [RadioIcon cell](./radio-icon)
- [RadioIconWidth cell](./radio-icon-width)
- [Type appendix](/docs/appx/type)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
