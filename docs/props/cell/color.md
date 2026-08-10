# Color ***(cell)***

<!-- synonyms: 셀 색상, 배경색, 셀 배경, 셀 컬러, HEX 색상, RGB 색상, 셀 배경색, 셀 컬러 지정, color, background color, cell-color, hex color, rgb color, cell background -->

> 셀의 배경 색상을 설정합니다.
>
> 색상은 상태에 따른 배경 색상의 영향을 받습니다.
>
> rgb(255,255,255)는 투명색이 됩니다.

### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`string`|HEX형식 (ex:#FF00F0)<br/>rgb형식 (ex:rgb(244,200,40)|

### Example

```javascript
//조회 데이터 내에서 속성 적용  (열이름 :CLS )
{
    data:[
        {... , "CLSColor":"#ADADAD" , ...}
    ]
}
```

### Read More
- [TextColor cell](./text-color)
- [TextStyle cell](./text-style)
- [TextSize cell](./text-size)
- [TextFont cell](./text-font)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
