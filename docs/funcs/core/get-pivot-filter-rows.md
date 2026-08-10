# getPivotFilterRows ***(method)***

<!-- synonyms: getPivotFilterRows, get-pivot-filter-rows, 피벗 필터, 원본 행, 피벗 시트, 필터링, pivot filter rows -->

> 피벗 시트에서 특정 셀의 데이터를 구성하는 원본 시트의 행을 가져오는 함수입니다.
>
> <mark>**주의!: 해당 API는 원본 시트의 필터링 내용을 제거합니다. API 사용시 원본 시트의 필터링 내용이 변경될 수 있습니다.**</mark>

### Syntax
```javascript
object getPivotFilterRows( row, col );
```

### Parameters
|Name|Type|Required| Description |
|----------|-----|---|----|
|row |`object`|<span class='required'>필수</span>|[데이터 로우 객체](/docs/appx/row-object)|
|col |`string`|<span class='required'>필수</span>|열이름|


### Return Value
***array[row object]*** : 필터된 원본 시트 [데이터 로우 객체](/docs/appx/row-object)들의 배열

### Example

```js
var focusRow = pivotSheet_sheet.getFocusedRow();
var focusCol = pivotSheet_sheet.getFocusedCol();

// 피벗 데이터를 구성하는 행을 가져오기
var datas = pivotSheet_sheet.getPivotFilterRows(focusRow, focusCol);
```

### Read More

- [makePivotTable method](./make-pivot-table)
- [switchPivotSheet method](./switch-pivot-sheet)
- [ClickPivotFilter](/docs/props/cfg/click-pivot-filter)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.28|기능 추가|
