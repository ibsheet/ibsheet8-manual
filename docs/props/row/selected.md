# Selected ***(row)***
> 행의 선택 상태를 설정하거나 확인합니다.
> `Selected`는 선택(Selection) 상태를 의미하며, `Focus`(현재 커서 위치)와는 별개입니다.

<!-- synonyms: row selected, selected row, row selection, selected state, selection status, 선택된 행, 행 선택 상태, 선택 여부, selected 속성 -->

### Type
`number`

### Options
|Value|Description|
|-----|-----|
| `0` | 선택되지 않음 |
| `1` | 행 전체가 선택됨 |
| `2` | 행의 일부 셀이 선택됨 (부분 선택) |

### Example
```javascript
// 1. 특정 행을 선택 상태로 설정
var row = sheet.getRowById("AR55");
row["Selected"] = 1;
// 화면에 선택 상태를 반영
sheet.refreshRow(row);

// 2. API를 이용해 특정 행 선택
var row = sheet.selectRow(sheet.getRowById("AR5"));

```

### Read More
- [SelectingCells cfg](/docs/props/cfg/selecting-cells)
- [selectRow method](/docs/funcs/core/select-row)
- [getSelectedRows method](/docs/funcs/core/get-selected-rows)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
