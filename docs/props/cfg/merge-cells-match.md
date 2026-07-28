# MergeCellsMatch ***(cfg)***

> 머지된 셀을 편집할 때, 머지 영역 전체의 값을 동시에 변경할지 여부를 설정하는 옵션입니다.  
> 머지 영역의 값이 동시에 변경되면 [onBeforeChange](/docs/events/on-before-change), [onAfterChange](/docs/events/on-after-change)는 **값이 변경된 각 셀마다** 발생합니다.

### 기본 동작 보충 설명
- **SearchMode: 0 / 3**
  - 머지된 영역을 편집하면 값이 변경되면서 머지가 해제됩니다.
  
- **SearchMode: 1 / 2**
  - 머지된 영역을 편집하면 **값은 변경되지만 머지는 유지됩니다.**
  - 편집(셀 값 변경, 행 추가 등) 이후에도 머지 상태를 다시 계산하려면 [EditAutoMerge](/docs/props/cfg/edit-auto-merge) 설정이 필요합니다.


### Type
`boolean`

### Options 
|Value|Description|
|-----|-----|
|`0(false)`|머지된 셀 편집 시 첫번째 셀의 값만 변경 (`default`)|
|`1(true)`|머지된 셀 편집 시 머지 영역 전체의 값을 동일하게 변경|

### Example
```javascript
options.Cfg = {
    MergeCellsMatch: true
};
```

### Read More
- [DataMerge cfg](/docs/props/cfg/data-merge)
- [MergeVisibleDom cfg](/docs/props/cfg/merge-visible-dom)
- [setValue method](/docs/funcs/core/set-value)
- [onBeforeChange event](/docs/events/on-before-change)
- [onAfterChange event](/docs/events/on-after-change)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.7|기능 추가|
|core|8.1.0.49|복사붙여넣기를 통한 값 변경에도 기능 적용|
