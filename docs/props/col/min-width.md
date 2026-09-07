# MinWidth ***(col)***

<!-- synonyms: 최소 너비, 최소 폭, 리사이즈 최소, 열 최소 크기, min width, minimum width, column min size, resize limit min -->

> 열의 최소 너비를 pixel단위로 설정합니다.  
> 사용자가 드래그로 열 너비를 조정할 때는 물론, [AutoFitColWidth](/docs/props/cfg/auto-fit-col-width)/[fitColWidth](/docs/funcs/core/fit-col-width)로 너비가 자동 조정될 때도 이 값보다 작아지지 않습니다.

### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`number`|열의 최소 너비(pixel단위)|


### Example
```javascript
// 초기 너비는 150px, 최소 너비는 110px로 설정
// (드래그나 자동 조정으로 줄여도 110px 아래로는 작아지지 않음)
options.Cols = [
    
    {Type: "Enum", Name: "DeptNm", Width: 150, MinWidth: 110},
   
];
```

### Read More
- [Width col](./width)
- [MaxWidth col](./max-width)
- [RelWidth col](./rel-width)
- [AutoFitColWidth cfg](/docs/props/cfg/auto-fit-col-width)
- [fitColWidth method](/docs/funcs/core/fit-col-width)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
