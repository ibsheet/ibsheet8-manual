# deleteRows ***(method)***

<!-- synonyms: 행 삭제, 로우 삭제, 다중 삭제, 삭제 상태, delete status, 삭제 플래그 -->

> 지정한 행들의 <mark>상태를 삭제로 변경</mark>합니다.  
> 행이 시트에서 실제로 제거되는 것이 아니라, [Deleted](/docs/props/row/deleted) 속성값이 `1`로 세팅됩니다.  
> 행을 시트에서 즉시 제거하려면 [removeRows](./remove-rows)를 사용하세요.  
> 트리의 경우 자식 행들도 함께 삭제 상태로 변경됩니다.

### Syntax
```javascript
boolean deleteRows( rows, del );
```

### Parameters
|Name|Type|Required|Description|
|----------|-----|---|----|
|rows|`array[object]`|<span class='required'>필수</span>|[데이터 로우 객체](/docs/appx/row-object) 배열|
|del|`number`|<span class='optional'>선택</span>|삭제 상태 변경 여부<br/>`0`:삭제 상태 해제<br/>`1`:삭제 상태로 변경 (`default`)<br/>`2`:삭제 상태로 변경 후 해당 행들 숨김 (Visible:`0(false)` 처리)|


### Return Value
***boolean*** : 상태 변경 여부 (삭제 또는 해제로 변경이 이루어지면 true, 변화가 없으면 false 리턴)

### Example
```javascript
//AR5,AR8 행에 대해 상태를 삭제로 변경한다.
sheet.deleteRows({"rows":[sheet.getRowById("AR5"), sheet.getRowById("AR8")],"del":1});
```

### Read More
- [deleteRow method](./delete-row)
- [removeRows method](./remove-rows)
- [onBeforeRowDelete event](../../events/on-before-row-delete)
- [onAfterRowDelete event](../../events/on-after-row-delete)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
