# CanSort ***(col)***

<!-- synonyms: 정렬 가능, 소팅 가능, 헤더 클릭 정렬, 정렬 제한, 소팅 잠금, sortable, column sort, sort disable, header sort -->

> 열의 소팅 가능 여부를 설정합니다.
>
> 사용자가 헤더 영역의 셀을 클릭시 소팅이 이루어지는데, 이를 허용할지 여부를 설정합니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|사용자 소팅 불가|
|`1(true)`|사용자 소팅 가능 (`default`)|


### Example
```javascript
//특정 열에 대해 소팅하지 못하게 막음
options.Cols = [
    ...
    {Type: "Int", Name: "Rank_Sales", CanSort: 0 ...},
    ...
];
```

### Read More
- [CanMove col](./can-move)
- [CanResize col](./can-resize)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
