# ColMerge ***(Cell)***

> 특정 셀을 병합 대상에서 제외하거나 포함할지 설정합니다.  
> 데이터에서는 `{컬럼Name}ColMerge:0` 형식으로 설정합니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|해당 셀을 병합 대상에서 제외|
|`1(true)`|해당 셀을 병합 대상에 포함|

### Example
```javascript
options.Cfg = {
    DataMerge: 3
};

options.Cols = [
    {Type: "Text", Header: "부서", Name: "dept"} // ColMerge 기본값 1(병합 대상)
];

// 조회 데이터
{Data: [
    // 부서 컬럼의 첫 번째 데이터는 머지하지 않음
    {dept: "영업부", deptColMerge: 0},
    {dept: "영업부"},
    {dept: "영업부"}
]}
```

### Read More

- [RowMerge row](/docs/props/row/row-merge)
- [ColMerge col](/docs/props/col/col-merge)
- [DataMerge cfg](/docs/props/cfg/data-merge)
- [HeaderMerge cfg](/docs/props/cfg/header-merge)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
