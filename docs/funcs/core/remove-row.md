# removeRow ***(method)***

<!-- synonyms: 행 제거, 로우 제거, 행 삭제, remove, 즉시 삭제 -->

> 지정한 행을 시트에서 <mark>즉시 제거</mark>합니다.  
> 삭제 상태만 변경하려면 [deleteRow](./delete-row)를 사용하세요.  
> 여러 행을 제거할 때는 [removeRows](./remove-rows)를 사용하는 것이 좋습니다.  
> 트리의 경우 자식 행들도 함께 제거됩니다.

### Syntax
```javascript
void removeRow( row, nomerge, norender );
```

### Parameters
|Name|Type|Required| Description |
|----------|-----|---|----|
|row|`object`|<span class='required'>필수</span>|[데이터 로우 객체](/docs/appx/row-object)|
|nomerge|`boolean`|<span class='optional'>선택</span>|[DataMerge cfg](/docs/props/cfg/data-merge) 값이 `0` 외의 값일 때, 머지 계산을 바로 할 것인지 여부<br/>`0(false)`:행 제거 후, 머지 계산 (`default`)<br/>`1(true)`:행 제거 후, 머지 계산 안함|
|norender|`boolean`|<span class='optional'>선택</span><mark>(사용주의)</mark>|즉시 화면에 반영할 것인지 여부<br/>해당 기능을 사용한 뒤, 다른 동작을 실행 할 경우 `renderBody()`를 반드시 먼저 실행 해야 합니다.<br/>`0(false)`:즉시 반영 (`default`)<br/>`1(true)`:반영 안함<br/>|

### Return Value
***none***

### Example
```javascript
// AR5 행을 제거합니다.
sheet.removeRow({row:sheet.getRowById("AR5")});

// 체크된 행들을 제거 합니다.
var rows = sheet.getRowsByChecked("chk");
for (var i = 0; i < rows.length; i++) {
    sheet.removeRow(rows[i], null, 1);
}
sheet.renderBody(); // 무조건 해주어야 다른 동작이 일어남.

var rows = sheet.getRowsByChecked("chk");
for (var i = 0; i < rows.length; i++) {
    sheet.removeRow(rows[i], null, 1);
}
sheet.renderBody(); // 무조건 해주어야 다른 동작이 일어남.
sheet.setAutoMerge(3,3,1); // 머지된 시트의 경우 머지 동작까지 다시 해줘야합니다.
```

### Read More
- [deleteRow method](./delete-row)
- [deleteRows method](./delete-rows)
- [removeRows method](./remove-rows)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.0.0.7|`norender` 추가|
