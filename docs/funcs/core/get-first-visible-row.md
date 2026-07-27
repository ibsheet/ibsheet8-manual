# getFirstVisibleRow ***(method)***

> `Visible`이 `1`인 최 상단행을 확인합니다.
>
> 트리 기능 사용시 row 인자를 설정하면 행이 갖고있는 자식행 중 보여지는 첫번째 자식행이 리턴됩니다.

### Syntax
```javascript
object getFirstVisibleRow( row );
```

### Parameters
|Name|Type|Required| Description |
|----------|-----|---|----|
|row|`object`|<span class='optional'>선택</span>|[데이터 로우 객체](/docs/appx/row-object)|


### Return Value
***row object*** : [데이터 로우 객체](/docs/appx/row-object)

### Example
```javascript
//AR12행의 첫번째 자식행을 리턴합니다.
var fchildrow = sheet.getFirstVisibleRow("AR12");
```

### Read More
- [getFirstRow method](./get-first-row)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
