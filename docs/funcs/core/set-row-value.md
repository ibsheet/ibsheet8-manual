# setRowValue ***(method)***

<!-- synonyms: setRowValue, set-row-value, 행 값 설정, 로우 값, 행 데이터, 행 단위 데이터, 데이터 설정, 행 값 변경, 데이터 입력, row value, set row, apply row, change row, row data -->

> 행 단위별 데이터를 설정합니다.  
> [getRowValue](/docs/funcs/core/get-row-value)로 추출한 데이터를 행 단위별로 set 할 수 있습니다.


### Syntax
```javascript
object setRowValue( row, data, render, noCalc );
```

### Parameters
|Name|Type|Required| Description |
|----------|-----|---|----|
|row|`object`|<span class='required'>필수</span>|데이터를 설정할 대상 행(row)|
|data|`object`|<span class='required'>필수</span>|JSON 형식의 데이터|
|render|`boolean`|<span class='optional'>선택</span>|즉시 화면 반영 여부(`default : true`)<br/>해당 기능을 `0(false)`로 사용했을 경우, `rerender()`를 실행해야 화면에 반영 됩니다.<br/>`0(false)` : 반영 안함<br/>`1(true)` : 즉시 반영 |
|calc|`boolean`|<span class='optional'>선택</span>|포뮬러 계산 여부(`default : true`)<br> 해당 기능을 `0(false)`로 사용했을 경우, `calculate()`를 실행해야 포뮬러 계산이 됩니다.<br/>`0(false)` : 반영 안함<br/>`1(true)` : 즉시 반영 |


### Return Value

***none***

### Example
```javascript
// ================================
// (Row) 데이터 덮어쓰기 예제
// ================================

// 5번째 행 가져오기 (row 객체의 id가 AR5이다.)
var row = sheet.getRowById("AR5");

// AR5 행의 데이터를 JSON 형식으로 추출
var data = sheet.getRowValue(row);

// 1번째 행 가져오기 (row 객체의 id가 AR1이다.)
var targetRow = sheet.getRowById("AR1");

// AR1 행의 데이터를 AR5 행의 값으로 덮어쓰기
sheet.setRowValue(targetRow, data);

// ================================
// 특정 행(Row) 데이터 JSON으로 업데이트 예제
// ================================

const data = {
  name: "홍길동",
  dept: "총무부",
  salary: 3500000,
  bonus: 500000
};

// ID가 "AR1"인 행(Row) 데이터를 JSON 방식으로 일부 업데이트
// JSON 객체에 포함되지 않은 다른 컬럼 값은 변경되지 않고 그대로 유지됩니다.
var targetRow = sheet.getRowById("AR1");
sheet.setRowValue(targetRow, data);

// ================================
// 헤더 여러 컬럼 값 일괄 변경 예제
// ================================

//최상단 행 가져오기
const hr = sheet.getRowById("Header"); 

sheet.setRowValue({
  row: hr,
  data: {
    SalesToday: "매출",
    SalesSum: "매출",
    CostToday: "비용",
    CostSum: "비용"
  },
  calc: false
});

// 헤더 텍스트 변경 후 경우에 따라 Merge 재적용
sheet.setAutoMerge( {headerMerge:2});
```

### Read More

- [getRowValue](/docs/funcs/core/get-row-value)
- [setValue](/docs/funcs/core/set-value)

### Since

|product|version|desc|
|---|---|---|
|core|8.1.0.25|기능 추가|
|core|8.3.0.45|render인자 추가|
|core|8.3.0.46|calc 인자 추가|