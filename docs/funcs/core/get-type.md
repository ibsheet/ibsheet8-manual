# getType ***(method)***
> 특정 셀에 설정된 Type 값을 확인합니다.

### Syntax
```javascript
string getType( row, col );
```

### Parameters

|Name|Type|Required| Description |
|----------|-----|---|----|
|row |`object`|<span class='required'>필수</span>|[데이터 로우 객체](/docs/appx/row-object)|
|col |`string`|<span class='required'>필수</span>|열이름|

### Return Value

***string*** : 셀의 타입 (`Text`, `Int`, `Float`, `Date` 등)

### Example
```javascript
// 현재 포커스된 셀의 타입 확인
var type = sheet.getType(sheet.getFocusedRow(), sheet.getFocusedCol());
console.log("셀 타입: " + type); // Text, Int, Float, Date 등

// 특정 셀의 타입에 따라 분기 처리
if (sheet.getType(row, "price") === "Int") {
    console.log("숫자 컬럼입니다.");
}
```

### Read More
- [getFormat method](./get-format)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
