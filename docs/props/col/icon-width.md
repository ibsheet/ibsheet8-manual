# IconWidth ***(col)***

<!-- synonyms: 아이콘 너비, 아이콘 폭, 아이콘 크기, 셀 아이콘 사이즈, icon width, icon size, icon area width, custom icon width -->

> 셀 좌측에 버튼을 표시하는 [Icon](./icon) 속성 사용 시, 커스텀 이미지를 사용하는 경우 버튼의 영역 너비를 설정합니다. 
>
> 너비는 pixel 단위로 설정됩니다.


### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`number`|셀 좌측 버튼의 너비.|


### Example
```javascript
options.Cols = [
    ...
    //셀의 좌측에 이미지로 버튼을 추가합니다.
    {Type: "Text", Name: "brnSaleAmt", Icon: "Icon", IconSrc: "/pcd/img/popIcon.png", IconWidth: 15, Width: 120 ...},
    ...
];
```

### Read More
- [Icon col](./icon)
- [IconSrc col](./icon-src)
- [IconWidth cell](../cell/icon-width)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
