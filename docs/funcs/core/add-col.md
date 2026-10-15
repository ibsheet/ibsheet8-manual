# addCol ***(method)***

<!-- synonyms: 열 추가, 컬럼 추가, 동적 열 추가, 열 삽입, 컬럼 생성, 열 만들기, add-col, addCol, add column, insert column, dynamic column, create column, 열 덧붙이기, 헤더 추가, add columns dynamically -->

> 이미 생성된 시트에 동적으로 열을 추가합니다.

### Syntax
```javascript
object addCol( name, section, pos, param, visible, render );
```

### Parameters
|Name|Type|Required|Description|
|----------|-----|---|----|
|name|`string`|<span class='required'>필수</span>|추가할 열 이름|
|section|`number`|<span class='optional'>선택</span>|추가될 영역<br/>`0`:좌측 영역<br/>`1`:가운데 영역 (`default`)<br/>`2`:우측영역|
|pos|`number`|<span class='optional'>선택</span>|section 내에 위치 (0부터 시작, -1입력시 우측 끝 열) (`default: 0`)|
|param|`object`|<span class='optional'>선택</span>|열의 속성 (ex : `{Type:"Text", Header:"타이틀", Width:120, CanEdit:0}` )<br/>열 이름은 `name` 인자로 넘기며, `param`에는 `Name`을 넣지 않습니다.|
|visible|`boolean`|<span class='optional'>선택</span>|생성 후 화면에 `Visible` 여부<br/>`0(false)`:감춤 (`default`)<br/>`1(true)`:보임<br/>생략하면 열이 감춰진 채 추가됩니다.|
|render|`boolean`|<span class='optional'>선택</span>|즉시 화면 반영 여부<br/>해당 기능을 `0(false)`로 사용했을 경우, 작업 마무리 시에 `rerender()`를 실행해야 화면에 반영됩니다.<br/>`0(false)`:반영 안함<br/>`1(true)`:즉시 반영 (`default`)|

### Return Value
***object*** : 생성된 열 객체(name 인자에 이미 존재하는 열 이름을 입력하는 경우 `null` 이 리턴됨)

### Example
```javascript
// 가운데 영역 마지막에 "memo" 열을 추가
sheet.addCol("memo", 1, -1, { Header: "비고", Type: "Text", Width: 150, CanEdit: 1 }, true);

// 여러 열을 추가할 때는 render 를 false 로 주고, 모두 추가한 뒤 한 번만 그립니다.
var adds = [
    { name: "confirm", param: { Header: "확인", Type: "Bool", Width: 60, CanEdit: 1 } },
    { name: "grade",   param: { Header: "등급", Type: "Text", Width: 80, CanEdit: 0 } }
];
for (var i = 0; i < adds.length; i++) {
    // 열 이름은 첫 번째 인자로 넘깁니다. param 에는 Name 을 넣지 않습니다.
    sheet.addCol(adds[i].name, 1, -1, adds[i].param, true, false);
}
sheet.rerender();
```

> 이미 존재하는 열 이름으로 호출하면 추가되지 않고 `null` 이 반환됩니다.  
> 열 구성 전체가 바뀌면 [IBSheet.create](/docs/static/create)로 다시 만드는 편이 단순합니다.

### Try it
- [Demo of addCol](https://jsfiddle.net/gh/get/library/pure/ibsheet/ibsheet8-manual-sample/tree/master/samples/method/addCol-DynamicCols/)

### Read More
- [addRow method](./add-row)
- [IBSheet.create static](/docs/static/create)
- [rerender method](./rerender)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.0.0.17|`render` 인자 추가|
