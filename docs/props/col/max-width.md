# MaxWidth ***(col)***

<!-- synonyms: 최대 너비, 최대 폭, 리사이즈 최대, 열 최대 크기, max width, maximum width, column max size, resize limit max -->

> 사용자가 마우스 드래그를 이용하여 열의 너비를 조정할 때, 늘릴수 있는 최대 열의 너비를 설정합니다.

### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`number`|열의 최대 너비(pixel단위)|


### Example
```javascript
//특정 열의 최대 너비를 120px로 설정합니다.
options.Cols = [
    ...
    {Type: "Date", Name: "em_date", MaxWidth: 120, ...},
    ...
];
```

### Read More
- [Width col](./width)
- [MinWidth col](./min-width)
- [RelWidth col](./rel-width)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
