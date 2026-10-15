# SubSumRowsArray ***(cfg)***

<!-- synonyms: SubSumRowsArray, sub sum rows array, subtotal rows array, 소계 행 배열, 소계 그룹 행, 소계 그룹 데이터, 소계행 정보, 소계 데이터 행, SubSumRow, SubSumGroupedRows, subtotal group rows -->

> [makeSubTotal](/docs/funcs/core/make-sub-total)로 소계를 생성했을 때 제공되는 **확인 전용** 속성으로, 생성된 소계행 정보를 배열로 가지고 있습니다.  
> 각 항목에는 소계행 객체와 그 소계에 속한 데이터 행 배열이 들어 있어, 소계행 기준으로 그룹의 데이터 행을 참조할 때 사용합니다.  
> **배열 자체의 정보를 변경**(항목 삭제·추가, 배열 비우기 등)하면 시트 동작에 문제가 생길 수 있습니다.  
> 소계를 생성하지 않았거나 [removeSubTotal](/docs/funcs/core/remove-sub-total)로 제거한 경우에는 빈 배열입니다.

### Type
`array[object]`

### Options
|Name|Type|Description|
|-----|-----|-----|
|`SubSumRow`|`object`|소계행 [데이터 로우 객체](/docs/appx/row-object)|
|`SubSumRowGroup`|`number`|소계행이 생성된 소계 설정의 인덱스 (`makeSubTotal`에 전달한 배열에서의 순서, 0부터 시작)|
|`SubSumGroupedRows`|`array[object]`|해당 소계에 속한 [데이터 로우 객체](/docs/appx/row-object) 배열|

### Example
```javascript
// 소계행의 captionCol에서 해당 소계 그룹의 데이터 행 수를 표시
sheet.makeSubTotal([
  {
    stdCol: "sDept",
    sumCols: "sSalary",
    captionCol: [
      {
        col: "sUnit",
        val: function (fr) {
          // 현재 소계행에 해당하는 항목을 찾음
          var subSumSet = fr.Sheet.SubSumRowsArray.filter(function (rowSet) {
            return rowSet.SubSumRow == fr.Row;
          });
          // 소계 그룹에 속한 데이터 행 수
          return subSumSet[0].SubSumGroupedRows.length + "명";
        }
      }
    ]
  }
]);

// 생성된 모든 소계행과 그룹 데이터 행 수 확인
sheet.SubSumRowsArray.forEach(function (item) {
  console.log(item.SubSumRow.id, item.SubSumGroupedRows.length);
});
```

### Read More
- [CumulateRowsArray cfg](./cumulate-rows-array)
- [makeSubTotal method](/docs/funcs/core/make-sub-total)
- [removeSubTotal method](/docs/funcs/core/remove-sub-total)
- [getSubTotalRows method](/docs/funcs/core/get-sub-total-rows)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
