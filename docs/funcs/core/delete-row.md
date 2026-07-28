# deleteRow ***(method)***

<!-- synonyms: 행 삭제, 로우 삭제, 삭제 상태, delete status, 삭제 플래그 -->

> 지정한 행의 <mark>상태를 삭제로 변경</mark>합니다.  
> 행이 시트에서 실제로 제거되는 것이 아니라, [Deleted](/docs/props/row/deleted) 속성값이 `1`로 세팅됩니다.  
> 행을 시트에서 즉시 제거하려면 [removeRow](./remove-row)를 사용하세요.  
> 트리의 경우 자식 행들도 함께 삭제 상태로 변경됩니다.

### Syntax
```javascript
boolean deleteRow( row , del , valid, visible);
```

### Parameters
|Name|Type|Required|Description|
|----------|-----|---|----|
|row|`object`|<span class='required'>필수</span>|[데이터 로우 객체](/docs/appx/row-object)|
|del|`number`|<span class='optional'>선택</span>|삭제 상태 변경 여부<br/>`0`:삭제 상태 해제<br/>`1`:삭제 상태로 변경 (`default`)|
|valid|`boolean`|<span class='optional'>선택</span>|삭제/해제 가능여부 확인<br/>(실제로 삭제/해제 되진 않고 가능/불가능 여부만 확인해서 리턴)<br/>`0(false)`:가능여부 확인 안함 (`default`)<br/>`1(true)`:가능여부 확인 사용|
|visible|`boolean`|<span class='optional'>선택</span>|삭제 상태 행을 화면에 보여줄지 여부<br/>`0(false)`:삭제 상태 행 감춤<br/>`1(true)`:삭제 상태 행 보임 (`default`)|


### Return Value
***boolean*** : 상태 변경여부 (삭제 또는 해제로 변경이 이루어지면 true, 변화가 없으면 false 리턴)

### Example
```javascript
//AR5 행에 대해 상태를 삭제로 변경한다.
sheet.deleteRow({row:sheet.getRowById("AR5"), del:1});
```

### Read More
- [deleteRows method](./delete-rows)
- [removeRow method](./remove-row)
- [onBeforeRowDelete event](../../events/on-before-row-delete)
- [onAfterRowDelete event](../../events/on-after-row-delete)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.1.0.38|visible 기능 추가|
