# getValue ***(method)***

<!-- synonyms: getValue, get-value, 셀 값, 값 조회, 원본 값, 저장 값, 값 확인, 값 가져오기, value, cell, raw -->

> 특정 셀의 값을 가져오는 함수입니다.
> 포맷과 구분자가 제거된 값을 반환합니다.
> `Type`이 `Enum`인 경우 화면 표출 텍스트가 아닌 `Enum` 속성에 설정된 코드값을 반환합니다.
> 화면에 표출되는 값이 필요하다면 [getString](/docs/funcs/core/get-string)을 사용하세요.

### Syntax
```javascript
mixed getValue( row, col );
```

### Parameters
|Name|Type|Required| Description |
|----|----|--------|-------------|
|row |`object`|<span class='required'>필수</span>|[데이터 로우 객체](/docs/appx/row-object)|
|col |`string`|<span class='required'>필수</span>|열이름|

### Return Value
***mixed ( `number` \| `string` )*** : 셀의 타입에 따른 실제 저장값 리턴

| 컬럼 타입 | 반환값 | 예시 |
|---------|--------|------|
| Enum | 저장 코드값 | `"01"` |
| Date | 구분자 없는 날짜 | `"20151231"` |
| Int / Float | 순수 숫자 | `212555` |
| 일반 Text | 저장값 그대로 | `"홍길동"` |

### Example
```javascript
var row = sheet.getFirstRow();

// 기본 사용
var name = sheet.getValue(row, "Name");           // "홍길동"

// Date 컬럼 - yyyyMMdd 형태로 추출
var startDate = sheet.getValue(row, "StartDate"); // "20151231"

// Enum 컬럼 - 코드값 추출 (표출 텍스트가 필요하면 getString 사용)
var genderCode = sheet.getValue(row, "Gender");   // "01"  (화면표출: "남성")

// json 형태로 사용
var endDate = sheet.getValue({row: row, col: "EndDate"});
```

### Read More
- [getString method](./get-string)
- [setString method](./set-string)
- [setValue method](./set-value)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
