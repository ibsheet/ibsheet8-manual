# getRowByIndex ***(method)***
> 인덱스를 기준으로 [데이터 로우 객체](/docs/appx/row-object)를 확인합니다.
>
> 인덱스는 `1`부터 시작
>
> 감춰진 행은 index계산에서 제외됩니다.

### Syntax
```javascript
object getRowByIndex( index );
```

### Parameters
|Name|Type|Required| Description |
|----------|-----|---|----|
|index|`number`|<span class='required'>필수</span>|행 인덱스(1부터 시작)|


### Return Value
***row object*** : [데이터 로우 객체](/docs/appx/row-object)

### Example
```javascript
//5번 index행의 데이터 로우 객체를 얻습니다.
var rowObj = sheet.getRowByIndex(5);
```

### Read More
- [getRowById method](./get-row-by-id)
- [getRowIndex method](./get-row-index)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
