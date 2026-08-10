# HideMobile ***(col)***

<!-- synonyms: 모바일 숨김, 모바일 감춤, 모바일 안 보임, 반응형 숨김, hide mobile, mobile hidden, hide on mobile, responsive hide -->

> 모바일 환경에서 열의 보임 감춤/여부를 설정합니다.
>
> **※ iPad Pro나 Surface Pro는 모바일로 분류되지 않습니다.**

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|열 보임 (`default`)|
|`1(true)`|열 감춤|

### Example
```javascript
// 특정 열을 모바일에서 감춤
options.Cols = [
    ...
    {Type: "Int", Name: "Product_Sales", HideMobile: true, ...},
    ...
];
```

### Read More

- [BreakPoint col](/docs/props/col/break-point)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
