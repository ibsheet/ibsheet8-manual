# addRow ***(method)***

<!-- synonyms: 행 추가, 로우 추가, 신규 행, 행 생성, add row -->

> 신규 행을 추가합니다.  
> 트리 기능 사용 시에는 `parent` 인자를 지정해야 원하는 레벨로 행을 추가할 수 있습니다.  
> 소계([makeSubTotal](./make-sub-total)) 그룹 안에 행을 추가해도 소계 계산에 반영되지 않습니다.

### Syntax
```javascript
object addRow( next, visible, focus, parent, init, render );
```

### Parameters
|Name|Type|Required|Description|
|----------|-----|---|----|
|next|`object`|<span class='optional'>선택</span>|[데이터 로우 객체](/docs/appx/row-object)<br/>(지정한 행의 위에 신규 행이 생성됨. 값이 없으면 맨 마지막행에 생성)|
|visible|`boolean`|<span class='optional'>선택</span>|생성된 행의 보임/감춤 설정<br/>`0(false)`:감춤<br/>`1(true)`:보임 (`default`)|
|focus|`boolean`|<span class='optional'>선택</span>|생성 후 생성된 행으로 포커스 이동 여부<br/>`0(false)`:포커스 이동 안함<br/>`1(true)`:포커스 이동 (`default`)|
|parent|`object`|<span class='optional'>선택</span>|[데이터 로우 객체](/docs/appx/row-object) (트리 사용시 부모에 해당하는 행 지정)|
|init|`object`|<span class='optional'>선택</span>|신규 행에 값/옵션 설정 객체|
|render|`boolean`|<span class='optional'>선택</span>|화면 갱신 여부<br/>`0(false)`:화면 갱신 안함 (이 경우 [onRowAdd](/docs/events/on-row-add) 이벤트가 발생하지 않음)<br/>`1(true)`:즉시 화면 갱신 (`default`)|

### Return Value
***object*** : 생성된 [데이터 로우 객체](/docs/appx/row-object)

### Example
```javascript
// 맨 위에 신규 행을 생성합니다.
sheet.addRow( {"next":sheet.getFirstRow()} )

// 현재 포커스가 위치한 행의 위에 신규 행을 생성합니다.
sheet.addRow( {"next":sheet.getFocusedRow()} );

// 현재 포커스가 위치한 행의 아래에 신규 행을 생성합니다.(focus 이동)
sheet.addRow( {"next":sheet.getNextRow(sheet.getFocusedRow())});

// 트리 사용시 현재 포커스가 위치한 행의 아래에 같은 레벨의 신규 행을 생성합니다.
var nextRow = sheet.getNextSiblingRow(sheet.getFocusedRow());
var parentRow = sheet.getFocusedRow().parentNode;
sheet.addRow( {"next":nextRow, "parent":parentRow} );

// 현재 포커스가 된 행의 자식 노드로 신규 행을 추가합니다.
// next 로 기준 행을 주지 않으면, 자식 노드 맨 마지막에 행이 추가됩니다.
sheet.addRow({"parent":sheet.getFocusedRow()});

// 현재 포커스가 위치한 행의 위에 신규 행을 생성합니다.
// 신규 행의 CONTRACTNO과 CARNO 열에 값을 설정합니다.
// 신규 행의 배경 색상을 빨간색으로 설정합니다.
sheet.addRow({"next":sheet.getFocusedRow(), "init":{"CONTRACTNO":"S155", "CARNO":"1234123", Color:"red"}});

// render:0으로 행 추가 후 Formula 계산 및 화면 반영
sheet.addRow({init:{X:1, Y:6}, render:0});
sheet.calculate(false, false); // Formula 계산 (렌더링 안함)
sheet.rerender();              // 한 번에 화면 반영
```
### Demo
- [addRow sample](https://codepen.io/ibsheet/pen/dygddxQ)

### Read More
- [addRows method](./add-rows)
- [removeRow method](./remove-row)
- [onRowAdd event](../../events/on-row-add)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.0.0.3|`init` 인자 추가|
|core|8.0.0.20|`render` 인자 추가|
  