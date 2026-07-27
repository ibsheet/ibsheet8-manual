# OrigSearchData ***(cfg)***

<!-- synonyms: 원본 데이터, 데이터 형변환, 타입 변환, 숫자 변환, 문자열 유지, 전역 형변환 차단 -->

> 시트 전체의 조회 데이터를 Row 객체에 저장할 때 **원본 데이터 타입을 보존할지** 여부를 설정합니다(열 선언과 무관하게 모든 열에 일괄 적용).  
> 기본값(`0`)은 숫자처럼 보이는 값은 문자열로 받았더라도 숫자형으로 자동 변환합니다.  
> `1`로 설정하면 변환 없이 서버가 보낸 **원본 타입 그대로** 저장합니다.  
> 개별 열 단위로 적용하려면 [OrigSearchData col](/docs/props/col/orig-search-data)을 사용하세요.  
> [getValue](/docs/funcs/core/get-value), [getString](/docs/funcs/core/get-string)에는 영향을 주지 않습니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|조회 데이터가 숫자처럼 보이면 숫자형으로 변환하여 저장 (`default`)|
|`1(true)`|조회 데이터가 숫자처럼 보여도 변환하지 않고 받은 타입 그대로 저장|

### Example
같은 값을 조회했을 때 `Cfg.OrigSearchData` 설정에 따라 `row["col"]`에 저장되는 타입이 어떻게 달라지는지 비교합니다(모든 열에 동일 적용).

```javascript
// 컬럼 선언 (열에는 OrigSearchData 미설정 — 시트 전체 설정으로 일괄 제어)
Cols: [
  { Name:"col1", Type:"Text" },   // Text 열
  { Name:"col2", Type:"Int" }     // Int 열
]

options.Cfg = { OrigSearchData: 1 };   // 시트 전체 적용 (0이면 자동 변환)

// 조회 데이터 (서버 응답)
{ "Data": [
  { col1:123,   col2:123   },   // 숫자 123
  { col1:"123", col2:"123" }    // 문자 "123"
] }
```

| 조회 데이터 | 컬럼 | 기본 (`0`) | `OrigSearchData:1` |
|---|---|---|---|
| 숫자 `123` | `col1` (Text) | `number` | `number` |
| 숫자 `123` | `col2` (Int) | `number` | `number` |
| 문자 `"123"` | `col1` (Text) | `number` | `string` |
| 문자 `"123"` | `col2` (Int) | `number` | `string` |

### Read More
- [OrigSearchData col](/docs/props/col/orig-search-data)
- [행 객체](/docs/appx/row-object)
- [시트 객체 구조](/docs/appx/init-structure)
- [loadSearchData method](/docs/funcs/core/load-search-data)
- [doSearch method](/docs/funcs/core/do-search)
- [getValue method](/docs/funcs/core/get-value)
- [getString method](/docs/funcs/core/get-string)

### Since

|product|version|desc|
|---|---|---|
|core|8.4.0.4|기능 추가|
