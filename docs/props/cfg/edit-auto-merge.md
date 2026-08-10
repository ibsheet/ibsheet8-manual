# EditAutoMerge ***(cfg)***

<!-- synonyms: EditAutoMerge, edit auto merge, auto merge on edit, realtime merge, merge on change, 편집 자동 병합, 편집 시 병합, 실시간 병합, 자동 머지, 편집 자동 머지, SearchMode 병합, 편집 후 머지, 편집 시 자동 병합 -->

> `SearchMode: 1 / 2`를 설정한 시트에서 머지된 셀을 편집(셀 값 변경, 행 추가 등)할 때, **실시간으로 자동 병합할지 여부**를 설정하는 옵션입니다.  
> `SearchMode: 0`에서는 편집 후 자동 병합이 기본 동작이므로 이 설정이 필요 없습니다.  
> 이 속성을 `true`로 설정하면, 각 셀 편집 시마다 병합 로직이 수행되므로 시트 성능이 느려질 수 있습니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|편집 시 자동 병합하지 않음 (`default`)|
|`1(true)`|편집 시 자동 병합 수행|


### Example
```javascript
options = {
    Cfg :{
      EditAutoMerge: true,  // 값 편집 시 자동 병합 수행
    }
};
```

### Read More
- [MergeCellsMatch cfg](./merge-cells-match)
- [DataMerge Cfg](/docs/props/cfg/data-merge)
- [addRow method](/docs/funcs/core/add-row)
- [addRows method](/docs/funcs/core/add-rows)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.0.0.5|행 추가 시 셀 병합이 되도록 수정|