# CanSort ***(cfg)***

> 헤더 클릭을 통한 열 정렬(Sort) 기능의 허용 여부를 설정합니다.  
> `Cfg.CanSort`가 `false`로 설정된 경우, `Row` 또는 `Col` 단위의 `CanSort` 설정은 적용되지 않습니다.  
> [SortIcons cfg](./sort-icons) 설정에 따라 헤더 정렬 아이콘을 숨길 수 있습니다.

<!-- synonyms: sort disable, disable sorting, header sort, column sort, 정렬 비활성화, 정렬 막기, 헤더 클릭 정렬 -->

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|정렬 기능 사용 안함|
|`1(true)`|정렬 기능 사용 (`default`)|


### Example
```javascript
options.Cfg = {
    CanSort: false,   //  헤더 클릭 정렬 비활성화
};
```

### Read More
- [CanSort row](/docs/props/row/can-sort)
- [CanSort col](/docs/props/col/can-sort)
- [HeaderSortActionMode cfg](./header-sort-action-mode) 
- [HeaderSortMode cfg](./header-sort-mode)
- [HighlightAfterSort cfg](./highlight-after-sort) 
- [MaxSort cfg](./max-sort)
- [SortIcons cfg](./sort-icons)
- [SortIconsNum cfg](./sort-icons-num) 


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
