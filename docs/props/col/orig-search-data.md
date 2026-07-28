# OrigSearchData ***(col)***

<!-- synonyms: 원본 데이터, 데이터 형변환, 타입 변환, 숫자 변환, 문자열 유지 -->

> 해당 열의 조회 데이터를 Row 객체에 저장할 때 **원본 데이터 타입을 보존할지** 여부를 설정합니다.  
> 기본값(`0`)은 숫자처럼 보이는 값은 문자열로 받았더라도 숫자형으로 자동 변환합니다.  
> `1`로 설정하면 변환 없이 서버가 보낸 **원본 타입 그대로** 저장합니다.  
> 시트 전체에 적용하려면 [OrigSearchData cfg](/docs/props/cfg/orig-search-data)를 사용하세요.  
> [getValue](/docs/funcs/core/get-value), [getString](/docs/funcs/core/get-string)에는 영향을 주지 않습니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|조회 데이터가 숫자처럼 보이면 숫자형으로 변환하여 저장 (`default`)|
|`1(true)`|조회 데이터가 숫자처럼 보여도 변환하지 않고 받은 타입 그대로 저장|

### Example
같은 값을 조회했을 때 컬럼 타입과 `OrigSearchData` 설정에 따라 `row["col"]`에 저장되는 타입이 어떻게 달라지는지 비교합니다.

```javascript
// 컬럼 선언
Cols: [
  { Name:"col1", Type:"Text" },                    // Text
  { Name:"col2", Type:"Text", OrigSearchData:1 },  // Text + Orig:1
  { Name:"col3", Type:"Int" },                     // Int
  { Name:"col4", Type:"Int",  OrigSearchData:1 }    // Int + Orig:1
]

// 조회 데이터 (서버 응답) — 같은 값을 네 열에 동일하게 전달
{ "Data": [
  { col1:123,   col2:123,   col3:123,   col4:123   },   // 숫자 123
  { col1:"123", col2:"123", col3:"123", col4:"123" }    // 문자 "123"
] }
```

| 조회 데이터 | `col1`<br>(Text) | `col2`<br>(Text+Orig:1) | `col3`<br>(Int) | `col4`<br>(Int+Orig:1) |
|---|---|---|---|---|
| 숫자 `123` | `number` | `number` | `number` | `number` |
| 문자 `"123"` | `number` | `string` | `number` | `string` |

### Read More
- [OrigSearchData cfg](/docs/props/cfg/orig-search-data)
- [행 객체](/docs/appx/row-object)
- [시트 객체 구조](/docs/start/basic-structure)
- [loadSearchData method](/docs/funcs/core/load-search-data)
- [doSearch method](/docs/funcs/core/do-search)
- [getValue method](/docs/funcs/core/get-value)
- [getString method](/docs/funcs/core/get-string)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.17|기능 추가|
