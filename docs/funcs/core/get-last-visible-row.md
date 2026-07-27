# getLastVisibleRow ***(method)***

> 보여지는 최 하단행(`Visible: 1`)인 속성을 확인합니다.
>
> 트리 기능 사용시 row 인자를 설정하면 행이 갖고있는 보여지는 마지막 자식행이 리턴됩니다.

### Syntax
```javascript
object getLastVisibleRow( row );
```

### Parameters
|Name|Type|Required| Description |
|----------|-----|---|----|
|row|`object`|<span class='optional'>선택</span>|[데이터 로우 객체](/docs/appx/row-object)|


### Return Value
***row object*** : [데이터 로우 객체](/docs/appx/row-object)

### Example
```javascript
//보여지는 최 하단행을 얻습니다.
var lrow = sheet.getLastVisibleRow();
```

### Read More
- [getLastRow method](./get-last-row)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
