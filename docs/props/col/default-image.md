# DefaultImage ***(col)***
> [Type](/docs/appx/type)이 `Img`인 컬럼에서 이미지를 로드할 때 서버에 이미지가 없어 로드에 실패한 경우 대체로 표시할 이미지를 설정합니다.  
> 셀에 이미지 값(URL)이 있으나 로드에 실패한 경우에 적용되며, 값 자체가 없는 경우(`null`, `undefined`, 데이터 없음)의 기본 이미지는 [DefaultValue](/docs/props/col/default-value)로 지정합니다.  
> **<mark>주의</mark> : Img 데이터에 Left, Top이 설정된 경우엔 DefaultImage가 적용되지 않습니다**


### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`string`|이미지 로드 실패시 대체할 이미지의 url|

### Example
```javascript
options.Cols = [
    ...
    // 대체 이미지 경로를 설정한다.
    {
       Header: "이미지",
       Type: "Img",
       Name: "sImgData",
       Width: 120,
       DefaultImage: "./image/defaultImage.png",
       ...
    },
];
```

### Read More
- [DefaultValue col](./default-value)
- [Type appendix](/docs/appx/type)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.18|기능 추가|
