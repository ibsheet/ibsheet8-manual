# getNextRow ***(method)***

<!-- synonyms: getNextRow, get-next-row, 다음 행, 아래 행, 다음 로우, 이동, next row, below row, move -->

> 지정한 행의 바로 아래 행을 리턴합니다.
>
> 마지막 행인 경우 `null`이 리턴됩니다.


### Syntax
```javascript
object getNextRow( row );
```

### Parameters
|Name|Type|Required| Description |
|----------|-----|---|----|
|row|`object`|<span class='required'>필수</span>|[데이터 로우 객체](/docs/appx/row-object)|


### Return Value
***row object*** :  [데이터 로우 객체](/docs/appx/row-object)

### Example
```javascript
//AR5행의 다음 행을 확인.
var row = sheet.getRowById("AR55");
var nrow = sheet.getNextRow(row);
```

### Read More
- [getPrevRow method](./get-prev-row)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
