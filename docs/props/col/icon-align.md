Align ***(col)***

<!-- synonyms: 아이콘 정렬, 아이콘 위치, 좌측 아이콘, 우측 아이콘, 버튼 위치, icon align, icon position, left right icon -->

> 셀에 표시되는 아이콘의 좌우 위치를 설정합니다.  
> [Icon](./icon) 속성으로 표시하는 버튼(혹은 체크박스)과 `Enum` 타입의 드롭다운 아이콘에 적용됩니다.  
> 기본은 셀 좌측이며, 우측에도 표시할 수 있습니다.



### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`Left`|셀 좌측에 `Icon` 표시 (`default`)|
|`Right`|셀 우측에 `Icon` 표시|


### Example
```javascript
options.Cols = [
    ...
    //Enum 버튼을 셀 우측에 표시한다.
    {Type: "Enum", Name: "brnSaleAmt", IconAlign: "Right", Enum: "|사장|부장|차장|과장", EnumKeys: "|AA|BB|CC|DD" ...},
    ...
];
```

### Read More
- [Icon col](./icon)
- [IconWidth col](./icon-width)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.4|기능 추가|
