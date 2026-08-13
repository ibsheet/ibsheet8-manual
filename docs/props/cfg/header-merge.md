# HeaderMerge ***(cfg)***

<!-- synonyms: HeaderMerge, header merge, header cell merge, merge header, header auto merge, 헤더 병합, 헤더 머지, 헤더 셀 병합, 헤더 값 병합, 헤더 병합 종류, DataMerge 헤더, setAutoMerge 헤더, 제목 병합 -->

> 시트 생성 시 헤더 영역에서 셀 값을 기준으로 병합할지 여부 및 병합 종류를 설정합니다.  
> 옵션에 대한 설명은 [DataMerge](./data-merge)와 동일합니다.  
> [ColMerge](/docs/props/col/col-merge) 설정과 관계없이 동작합니다. 헤더에서도 ColMerge를 따르려면 [IgnoreHeaderColMerge](./ignore-header-col-merge)를 `0(false)`으로 설정하세요.  
> 시트 생성 후 [setAutoMerge](/docs/funcs/core/set-auto-merge) 메소드를 이용하여 헤더 영역의 병합을 동적으로 변경할 수 있습니다.  
> [Span](/docs/props/cell/span), [RowSpan](/docs/props/cell/row-span)은 적용되지 않습니다.

### Type
`number`

### Options
|Value|Description|
|-----|-----|
| `0` | 병합 안 함 (`default`)|
| `1` | 열 기준 병합|
| `2` | 행 기준 병합|
| `3` | 열 우선 병합|
| `4` | 행 우선 병합|
| `5` | 열 우선 사방 병합|
| `6` | 행 우선 사방 병합|

### Example
```javascript
options = {
    Cfg :{
        HeaderMerge: 0,  // 시트 생성 시 헤더 영역의 셀 병합을 진행하지 않습니다.
    }
};
```

### Try it
- [0 by default with setAutoMerge](https://jsfiddle.net/gh/get/library/pure/ibsheet/ibsheet8-manual-sample/tree/master/samples/properties/Cfg/Merge/)

### Read More
- [DataMerge cfg](./data-merge)
- [PrevColumnMerge cfg](./prev-column-merge)
- [IgnoreHeaderColMerge cfg](./ignore-header-col-merge)
- [ColMerge col](/docs/props/col/col-merge)
- [Span cell](/docs/props/cell/span)
- [RowSpan cell](/docs/props/cell/row-span)
- [setAutoMerge method](/docs/funcs/core/set-auto-merge)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
