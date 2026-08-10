# getFirstRow ***(method)***

<!-- synonyms: getFirstRow, get-first-row, 첫 행, 첫번째 행, 최상단 행, 시작 행, 첫 로우, 첫 자식 행, first, row, top -->

> 최 상단행을 확인합니다.
>
> 트리 기능 사용시 row 인자를 설정하면 행이 갖고있는 첫번째 자식행이 리턴됩니다.

### Syntax
```javascript
object getFirstRow( row );
```

### Parameters
|Name|Type|Required| Description |
|----------|-----|---|----|
|row|`object`|<span class='optional'>선택</span>|[데이터 로우 객체](/docs/appx/row-object)|


### Return Value
***row object*** : [데이터 로우 객체](/docs/appx/row-object)

### Example
```javascript
//최 상단행을 얻습니다.
var frow = sheet.getFirstRow();
```

### Read More
- [getFirstVisibleRow method](./get-first-visible-row)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
