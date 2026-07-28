# startEdit ***(method)***

<!-- synonyms: 편집모드, 편집 시작, 셀 편집, edit start, startedit -->

> 셀의 편집모드로 진입합니다.  
> 지정한 셀에 커서가 깜빡이는 편집상태가 활성화됩니다.  
> `row, col` 인자를 설정하지 않으면 포커스가 있는 셀이 편집상태로 변경됩니다.

### Syntax
```javascript
void startEdit( row, col, empty, valid );
```

### Parameters
|Name|Type|Required|Description|
|----------|-----|---|----|
|row |`object`|<span class='optional'>선택</span>|편집할 [데이터 로우 객체](/docs/appx/row-object)|
|col |`string`|<span class='optional'>선택</span>|편집할 열이름|
|empty |`boolean`|<span class='optional'>선택</span>|편집 시작시 기존 셀의 값을 지울지 여부<br>`0(false)`:편집 시작 시 기존 셀의 값 유지 (`default`)<br>`1(true)`:편집 시작시 기존 셀의 값 제거|
|valid |`boolean`|<span class='optional'>선택</span>|셀의 편집 가능여부 확인<br>(실제로 셀이 편집상태가 활성화 되지 않고, 편집상태로 활성화가 가능/불가능 여부를 확인해서 리턴. 이미 활성화 되어 있는 경우 `0(false)`를 리턴)<br>`0(false)`:셀의 편집 가능여부 확인 안함 (`default`)<br>`1(true)`:셀의 편집 가능여부 확인 사용|

### Return Value
***none***

### Example
```javascript
// 포커스된 셀에서 편집 시작 (인자 생략)
sheet.startEdit();

// 특정 셀 편집 시작 (positional)
sheet.startEdit(sheet.getRowById("AR5"), "CARNO");

// 객체 형식도 사용 가능 (positional과 동일)
sheet.startEdit({row: sheet.getRowById("AR5"), col: "CARNO"});

// 현재 포커스된 셀에서 편집 시작 + 기존 값 제거 (객체 형식이 부분 인자 지정에 편리)
sheet.startEdit({empty: 1});

// 편집 가능 여부만 확인 (실제 편집은 시작하지 않음)
var canEdit = sheet.startEdit(row, col, 0, 1);
```

### Read More

- [focus method](./focus)
- [endEdit method](./end-edit)
- [onStartEdit event](/docs/events/on-start-edit)
- [onShowEdit event](/docs/events/on-show-edit)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
