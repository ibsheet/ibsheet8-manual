# getMergeRange ***(method)***
> 특정 셀을 기준으로 머지된 영역(RowSpan, Span)을 확인합니다.  
> 지정한 셀을 기준으로 머지 시작셀(좌측 상단)과 종료셀(우측 하단)을 배열로 리턴합니다.

### Syntax
```javascript
array getMergeRange( row, col);
```

### Parameters
|Name|Type|Required| Description |
|----------|-----|---|----|
|row |`object`|<span class='required'>필수</span>|병합기준 [데이터 로우 객체](/docs/appx/row-object)|
|col |`string`|<span class='required'>필수</span>|병합기준 열이름|

### Return Value
***array*** : `[시작행, 시작열이름, 종료행, 종료열이름]`

머지되지 않은 셀의 경우 시작과 종료가 동일한 값으로 리턴됩니다.

### Example
```javascript
//AR2행, deptCd열이 주변과 병합된 경우 병합영역을 리턴
var mergeArr = sheet.getMergeRange( sheet.getRowById("AR2"), "deptCd");

var mergeStartRow = mergeArr[0]; // 머지 시작 행
var mergeStartCol = mergeArr[1]; // 머지 시작 열
var mergeEndRow = mergeArr[2]; // 머지 종료 행
var mergeEndCol = mergeArr[3]; // 머지 종료 열
```

### Read More
- [setMergeRange method](./set-merge-range)
- [setMergeCancel method](./set-merge-cancel)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.7|기능 추가|
