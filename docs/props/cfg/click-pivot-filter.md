# ClickPivotFilter ***(cfg)***
> 피벗 기능을 통해 생성된 피벗 시트에서 셀 데이터를 클릭했을 때,  
> 해당 값에 포함된 원본 시트의 행을 자동으로 필터링하여 표시할지 여부를 설정합니다.
>
> 이 옵션을 사용하면 피벗 결과를 기준으로  
> 원본 데이터의 상세 내역을 바로 확인할 수 있습니다.  
> 필터된 상태에서 원본 전체 데이터를 다시 보려면  
> [clearFilter](/docs/funcs/core/clear-filter) 메서드를 호출해야 합니다.

<!-- synonyms: pivot drill down, pivot click filter, pivot to original filter, 피벗 클릭 원본 필터, 피벗 드릴다운 -->

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0`(`false`)|피벗 클릭 시 원본 시트 필터 기능 사용 안 함 (`default`)|
|`1`(`true`)|피벗 클릭 시 원본 시트에 자동 필터 적용|


### Example
```javascript
options = {
  "Cfg":{
    "ClickPivotFilter": 1,  // 피벗 시트 클릭 필터 기능 사용
  }
};
```

### Read More
- [clearFilter method](/docs/funcs/core/clear-filter)
- [getPivotFilterRows method](/docs/funcs/core/get-pivot-filter-rows)
- [makePivotTable method](/docs/funcs/core/make-pivot-table)
- [switchPivotSheet method](/docs/funcs/core/switch-pivot-sheet)
- [UsePivot cfg](./use-pivot)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.20|기능 추가|
