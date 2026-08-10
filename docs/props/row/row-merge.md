# RowMerge ***(row)***

<!-- synonyms: row merge, horizontal merge, per-row data merge, header merge exclude, cell value merge, dataMerge target, 가로 병합, 좌우 병합, 값 기준 병합, 데이터 병합 대상, 헤더 병합 대상, RowMerge 속성 -->

> 데이터 영역/헤더 영역에서 값 기준 병합 실행([DataMerge](/docs/props/cfg/data-merge), [HeaderMerge](/docs/props/cfg/header-merge)) 시 해당 행의 가로(좌우) 병합 여부를 설정합니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|해당 행을 병합 대상에 포함하지 않습니다.|
|`1(true)`|해당 행을 병합 대상에 포함합니다. (`default`)|

### Example
```javascript
options.Cfg = {
    DataMerge: 3,   // 열+행 병합
    HeaderMerge: 3
};

// 조회 데이터에서 특정 행 가로 머지 제외
{Data: [
    {RowMerge: 0, dept: "영업부", name: "영업부"},  // 이 행은 가로 머지하지 않음
    {dept: "영업부", name: "영업부"},                // 이 행은 가로 머지 대상
]}

```

### Read More
- [ColMerge col](/docs/props/col/col-merge)
- [ColMerge cell](/docs/props/cell/col-merge)
- [DataMerge cfg](/docs/props/cfg/data-merge)
- [HeaderMerge cfg](/docs/props/cfg/header-merge)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
