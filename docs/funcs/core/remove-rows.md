# removeRows ***(method)***

<!-- synonyms: 행 제거, 로우 제거, 다중 제거, 행 삭제, remove, 즉시 삭제 -->

> 지정한 여러 행들을 시트에서 <mark>즉시 제거</mark>합니다.  
> 삭제 상태만 변경하려면 [deleteRows](./delete-rows)를 사용하세요.  
> 트리의 경우 자식 행들도 함께 제거됩니다.

### Syntax
```javascript
void removeRows( rows );
```

### Parameters
|Name|Type|Required| Description |
|----------|-----|---|----|
|rows|`array[object]`|<span class='required'>필수</span>|제거하고자 하는 행들|

### Return Value
***none***

### Example
```javascript
// 체크된 행들을 제거 합니다.
var rows = sheet.getRowsByChecked("chk");
sheet.removeRows(rows);
```

### Read More
- [removeRow method](./remove-row)
- [deleteRows method](./delete-rows)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.7|기능 추가|
