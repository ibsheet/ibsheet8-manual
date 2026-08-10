# ButtonWidth ***(row)***

<!-- synonyms: button width, row button width, cell button width, button size, button pixel width, 버튼 너비, 버튼 폭, 버튼 크기, 셀 버튼 너비, 행 버튼 너비, ButtonWidth 속성 -->
> 설정한 `row`에 생성되는 버튼 객체의 너비를 설정합니다.
> [Type](/docs/props/col/type)이 `Button`이고, [Button](/docs/props/col/button)속성의 값이 `Button`인 조건을 만족한 버튼 객체에만 설정됩니다.

### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`number`|버튼 태그의 너비(pixel단위)|

### Example
```javascript
//특정행에 버튼의 너비를 16px로 설정
var rows = sheet.getDataRows();
rows[3]["ButtonWidth"] = "16px";
sheet.refreshRow(rows[3]);
```

### Read More
- [Type col](/docs/props/col/type)
- [Button col](/docs/props/col/button)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
