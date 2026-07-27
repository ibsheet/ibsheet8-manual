# getRowIndex ***(method)***
> [데이터 로우 객체](/docs/appx/row-object)의 인덱스를 반환합니다.
>
> 인덱스는 `1`부터 시작합니다.
>
> [Visible](/docs/props/row/visible):0 인 Row는 인덱스가 반환되지 않습니다.


### Syntax
```javascript
number getRowIndex( row );
```

### Parameters
|Name|Type|Required| Description |
|----------|-----|---|----|
|row|`object`|<span class='required'>필수</span>|[데이터 로우 객체](/docs/appx/row-object)|


### Return Value
***number*** : 행의 index

### Example
```javascript
//AR5 행의 index를 확인합니다.
var row = sheet.getRowById("AR5");
var idx = sheet.getRowIndex(row);
```

### Read More
- [getRowById method](./get-row-by-id)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
