# getSubTotalRows ***(method)***

> 생성된 소계/누계 행들을 반환합니다.

### Syntax
```javascript
object getSubTotalRows();
```

### Return Value
***object***

|Name|Type|Description|
|---|---|---|
|subTotal|`array[array]`|기준열별 소계행 배열|
|Total|`array[array]`|기준열별 누계행 배열|

### Example
```javascript
var result = sheet.getSubTotalRows();
// result.subTotal — 기준열별 소계행 배열
// result.Total    — 기준열별 누계행 배열
```

### Read More
- [makeSubTotal method](./make-sub-total)
- [removeSubTotal method](./remove-sub-total)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
