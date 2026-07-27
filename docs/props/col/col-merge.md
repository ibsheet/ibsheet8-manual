# ColMerge ***(col)***

<!-- synonyms: 컬럼 머지, 열 병합, 가상 머지, 시각적 머지, virtual merge -->

> 지정한 열 내에 상하 같은 값에 대해서 자동 병합 여부를 설정합니다.  
> `0`으로 설정 시 [PrevColumnMerge](/docs/props/cfg/prev-column-merge)(앞 열 기준 머지)의 대상에서도 제외됩니다.  
> `2`로 설정하면 시각적으로는 머지된 것처럼 보이지만 셀 단위로 개별 선택/포커스/편집이 가능한 가상 머지로 동작합니다.  
> 데이터 영역의 병합에만 영향을 미치며, 헤더 영역의 병합에는 영향을 미치지 않습니다.

### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`0`|해당 열을 병합하지 않습니다. (앞 열 병합 대상에서도 제외)|
|`1`|해당 열을 병합 대상에 포함합니다. (`default`)|
|`2`|시각적으로는 머지된 것처럼 보이지만 셀 단위로 개별 선택/포커스/편집이 가능한 가상 머지로 동작합니다.|

### Example
```javascript
options.Cols = [
    ...
    // 일반 머지에서 제외
    {Type: "Text", Name: "Dept", ColMerge: 0, Width: 100},

    // 가상 머지 — 같은 값이 위아래로 이어지는 셀이 시각적으로 합쳐 보이지만,
    // 각 셀을 개별적으로 클릭/편집할 수 있음
    {Type: "Text", Name: "Region", ColMerge: 2, Width: 120},
    ...
];
```

### Read More

- [RowMerge row](/docs/props/row/row-merge)
- [ColMerge cell](/docs/props/cell/col-merge)
- [PrevColumnMerge cfg](/docs/props/cfg/prev-column-merge)
- [DataMerge cfg](/docs/props/cfg/data-merge)
- [HeaderMerge cfg](/docs/props/cfg/header-merge)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.4.0.5|값 `2`(가상 머지) 추가|
