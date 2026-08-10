# TextColor ***(cell)***

<!-- synonyms: 글자색, 글자 색상, 텍스트 색, 텍스트 색상, 폰트 색, 폰트 컬러, 글씨 색, 셀 글자색, HEX 색상, RGB 색상, text color, font color, foreground color, color -->

> 지정한 셀에 글자색을 설정합니다.

### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`string`|HEX형식 (ex:#FF00F0)<br/>rgb형식 (ex:rgb(244,200,40)|

### Example
```javascript
//1. 메소드를 통해 특정 셀에 속성 적용 (열이름: CLS)
sheet.setAttribute(sheet.getRowById("AR99"), "CLS", "TextColor", "#FF0000");


//2. 객체에 직접 접근해서 속성 적용 (열이름: CLS)
var ROW = sheet.getRowById("AR10");
ROW["CLSTextColor"] = "#AD4499";
//변경내용 확인
sheet.refreshCell({row:ROW, col:"CLS"});


//3. 조회 데이터 내에서 속성 적용  (열이름: CLS)
{
    data:[
        {... , "CLSTextColor": "#0000FF", ...}
    ]
}
```

### Read More
- [TextStyle cell](./text-style)
- [TextSize cell](./text-size)
- [TextFont cell](./text-font)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
