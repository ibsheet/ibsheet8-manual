# Orig ***(cell)***

<!-- synonyms: Orig, 원본 값, 최초 값, 원래 데이터, 최초 로딩 데이터, 원본 데이터, 초기값, 셀 원본, original value, original data, initial data, load value -->

> 셀에 **최초 로딩된 값**을 담고 있습니다.  
> 셀을 여러 번 편집해도 처음 값이 유지되며(직전 값이 아님), 수정 전 원본과 비교하거나 되돌릴 때 사용합니다.

### Type
`mixed`( `string` \| `number` )

원본 셀 값을 그대로 담으므로 반환 타입은 컬럼 `Type`을 따릅니다 (예: `Text`는 `string`, `Int`/`Float`는 `number`).

### Options
|Value|Description|
|-----|-----|
|`Orig`|처음 로딩된 데이터|


### Example
```javascript
//수정하기 전, 최초 데이터를 확인한다.
var orgValue = sheet.getAttribute(sheet.getRowById("AR99"), "CLS", "Orig");
```

### Read More
- [revertCell method](/docs/funcs/core/revert-cell)
- [revertRow method](/docs/funcs/core/revert-row)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
