# CumulateRowsArray ***(cfg)***

<!-- synonyms: CumulateRowsArray, cumulate rows array, cumulative rows array, 누계 행 배열, 누계행 목록, 누계행 정보, 누계 데이터 행, cumulative total rows -->

> [makeSubTotal](/docs/funcs/core/make-sub-total)에서 `showCumulate`로 누계행을 생성했을 때 제공되는 **확인 전용** 속성으로, 생성된 누계행 객체를 배열로 가지고 있습니다.  
> **배열 자체의 정보를 변경**(항목 삭제·추가, 배열 비우기 등)하면 시트 동작에 문제가 생길 수 있습니다.  
> 누계행을 생성하지 않았거나 [removeSubTotal](/docs/funcs/core/remove-sub-total)로 제거한 경우에는 빈 배열입니다.

### Type
`array[object]`

### Options
|Name|Type|Description|
|-----|-----|-----|
|(배열 항목)|`object`|누계행 [데이터 로우 객체](/docs/appx/row-object)|

### Example
```javascript
sheet.makeSubTotal([
  {
    stdCol: "sDept",
    sumCols: "sSalary",
    showCumulate: 1
  }
]);

// 생성된 누계행의 id와 누계 값 확인
sheet.CumulateRowsArray.forEach(function (row) {
  console.log(row.id, row.sSalary);
});
```

### Read More
- [SubSumRowsArray cfg](./sub-sum-rows-array)
- [makeSubTotal method](/docs/funcs/core/make-sub-total)
- [removeSubTotal method](/docs/funcs/core/remove-sub-total)
- [getSubTotalRows method](/docs/funcs/core/get-sub-total-rows)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
