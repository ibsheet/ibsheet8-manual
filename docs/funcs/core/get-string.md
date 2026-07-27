# getString ***(method)***
> 포맷이 적용된 문자열로 셀의 값을 가져옵니다.  
> [getValue](/docs/funcs/core/get-value)가 실제 저장값을 반환하는 것과 달리, `getString`은 화면에 표출되는 값을 반환합니다.  
> Enum 컬럼의 경우 저장된 코드값 대신 화면에 표출되는 텍스트를 반환합니다.  

### Syntax
```javascript
string getString( row, col);
```

### Parameters

|Name|Type|Required| Description |
|----------|-----|---|----|
|row |`object`|<span class='required'>필수</span>|[데이터 로우 객체](/docs/appx/row-object)|
|col |`string`|<span class='required'>필수</span>|열이름|

### Return Value
***string*** : 화면에 표출되는 포맷 적용된 문자열 리턴

| 컬럼 타입 | getValue | getString |
|---------|---------|---------|
| Enum | 저장 코드값 (`"01"`) | 표출 텍스트 (`"남성"`) |
| Date | 구분자 없는 날짜 (`"20151231"`) | 포맷 적용 날짜 (`"2015-12-31"`) |
| Int / Float | 순수 숫자 (`212555`) | 구분자 포함 (`"212,555"`) |
| 일반 Text | 저장값 | 저장값 (동일) |

### Example
```javascript
var row = sheet.getFirstRow();

// Enum 컬럼 - 저장값과 표출값 비교
var code = sheet.getValue(row, "GenderCol");    // "01"
var text = sheet.getString(row, "GenderCol");   // "남성"

// Date 컬럼 - 포맷 적용 여부 비교
var rawDate = sheet.getValue(row, "StartDate");    // "20151231"
var fmtDate = sheet.getString(row, "StartDate");   // "2015-12-31"

// Int 컬럼 - 구분자 포함 여부 비교
var rawNum = sheet.getValue(row, "Salary");    // 212555
var fmtNum = sheet.getString(row, "Salary");   // "212,555"
```

### Read More

- [setString method](./set-string)
- [setValue method](./set-value)
- [getValue method](./get-value)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
