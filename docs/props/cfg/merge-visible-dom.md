# MergeVisibleDom ***(cfg)***

> [SearchMode](/docs/props/cfg/search-mode):0, [MergeCellsMatch](/docs/props/cfg/merge-cells-match):1 환경에서 머지 영역이 화면 밖까지 이어지는 경우, 값을 편집하면 보이는 영역만 변경됩니다.  
> `0(false)`로 설정하면 보이지 않는 영역까지 값이 변경됩니다.
<!-- 해당 기능은 자동 머지([DataMerge](/docs/props/cfg/data-merge))를 이용한 머지 영역에서만 동작됩니다. <br> -->

### Type
`boolean`

### Options 
|Value|Description|
|-----|-----|
|`0(false)`|보이지 않는 영역까지 포함하여 병합|
|`1(true)`|보이는 영역만 병합 (`default`)|

### Example
```javascript
options.Cfg = {
    MergeVisibleDom: false
};
```

### Read More
- [SearchMode cfg](/docs/props/cfg/search-mode)
- [DataMerge cfg](/docs/props/cfg/data-merge)
- [MergeCellsMatch cfg](/docs/props/cfg/merge-cells-match)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.26|기능 추가|
