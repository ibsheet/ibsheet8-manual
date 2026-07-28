# CalcMergeMode ***(cfg)***
> [makeSubTotal](/docs/funcs/core/make-sub-total)(소계) 또는 [FormulaRow](/docs/props/col/formula-row)(합계) 사용 시, 머지된 셀을 하나의 값으로 계산할지 여부를 설정합니다.  
> 기본적으로는 머지된 셀을 각각 개별 값으로 계산합니다.

<!-- synonyms: makeSubTotal, FormulaRow, merged cell, 소계, 합계, cell merge, 셀병합, 머지 -->

### 동작 보충 설명
- 값 수정 후에도 머지된 셀을 하나의 값으로 계산하려면   
  [MergeCellsMatch](/docs/props/cfg/merge-cells-match) 및 [EditAutoMerge](/docs/props/cfg/edit-auto-merge) 설정을 함께 사용해야 합니다.


### 옵션별 동작 이미지
![다운로드](/assets/imgs/nonCalcMergeMode.png)
> **CalcMergeMode: 0** — 소계 및 합계 계산 시 머지된 셀을 **각 Row별로 계산**합니다. (`default`)


![다운로드](/assets/imgs/CalcMergeMode.png)
> **CalcMergeMode: 1~3** — 설정값에 따라 머지된 셀을 **하나의 값으로 계산**합니다.  

### Type
`number`

### Options
|Value|Description|
|-----|------|
|`0`|소계 및 합계 계산 시 머지된 셀을 **Row별 값으로 계산** (`default`)|
|`1`|소계 계산 시 머지된 셀을 **하나의 값으로 계산**(`makeSubTotal` 전용)|
|`2`|합계 계산 시 머지된 셀을 **하나의 값으로 계산**(`FormulaRow` 전용)|
|`3`|소계 및 합계 모두 머지된 셀을 **하나의 값으로 계산**|

### Example
```javascript
options.Cfg = {CalcMergeMode: 1};
sheet.makeSubTotal({...});
```

### Read More
- [makeSubTotal method](/docs/funcs/core/make-sub-total)
- [FormulaRow col](/docs/props/col/formula-row)
- [SearchMode cfg](/docs/props/cfg/search-mode)
- [EditAutoMerge cfg](/docs/props/cfg/edit-auto-merge)
- [MergeCellsMatch cfg](/docs/props/cfg/merge-cells-match)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.5|기능 추가|
|core|8.0.0.8|SearchMode:0에서 동작하게 수정|
|core|8.0.0.11|CalcMergeMode: 2/3 추가|