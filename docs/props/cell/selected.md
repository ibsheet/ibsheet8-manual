# Selected ***(cell)***

> 셀의 선택 상태를 설정하거나 확인합니다.  
> 이 속성은 `SelectingCells:1` 설정에서 사용할 수 있습니다.
>
> ※ `Selected`는 선택(Selection) 상태를 의미하며,  
> `Focus`(현재 활성 셀 표시)와는 별개입니다.

<!-- synonyms: cell selected, selected cell, cell selection, selection state, 선택된 셀, 셀 선택 상태, Selected 속성 -->


### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|셀 선택 해제|
|`1(true)`|셀 선택|

### Example
```javascript
//특정 셀을 선택한다.
sheet.selectCell(  sheet.getRowById("AR9"),
  "CLS",
  1
);

```

### Read More
- [Selected row](/docs/props/row/selected)
- [SelectingCells cfg](/docs/props/cfg/selecting-cells)
- [selectCell method](/docs/funcs/core/select-cell)
- [getSelectedRanges method](/docs/funcs/core/get-selected-range)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
