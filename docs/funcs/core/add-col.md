# addCol ***(method)***

<!-- synonyms: 열 추가, 컬럼 추가, 동적 열 추가, 열 삽입, 컬럼 생성, 열 만들기, add-col, addCol, add column, insert column, dynamic column, create column -->

> 이미 생성된 시트에 동적으로 열을 추가합니다.

### Syntax
```javascript
object addCol( name, section, pos, param, visible, render );
```

### Parameters
|Name|Type|Required|Description|
|----------|-----|---|----|
|name|`string`|<span class='required'>필수</span>|추가할 열이름|
|section|`number`|<span class='optional'>선택</span>|추가될 영역<br/>`0`:좌측 영역<br/>`1`:가운데 영역 (`default`)<br/>`2`:우측영역|
|pos|`number`|<span class='optional'>선택</span>|section 내에 위치 (0부터 시작, -1입력시 우측 끝 열) (`default: 0`)|
|param|`object`|<span class='optional'>선택</span>|열의 속성 (ex : `{Type:"Text", Header:"타이틀", Width:120, CanEdit:0}` )
|visible|`boolean`|<span class='optional'>선택</span>|생성 후 화면에 `Visible` 여부<br/>`0(false)`:감춤 (`default`)<br/>`1(true)`:보임|
|render|`boolean`|<span class='optional'>선택</span>|즉시 화면 반영 여부<br/>해당 기능을 `0(false)`로 사용했을 경우, 작업 마무리 시에 `rerender()`를 실행해야 화면에 반영 됩니다.<br/>`0(false)`:반영 안함<br/>`1(true)`:즉시 반영 (`default`)|

### Return Value
***object*** : 생성된 열 객체(name 인자에 이미 존재하는 열이름을 입력하는 경우 `null` 이 리턴됨)

### Example
```javascript
// 가운데 영역 마지막 열으로 "Name:EXT_SUBSUM" 열을 추가
sheet.addCol( "EXT_SUBSUM", 1, -1, {Type:"Int",Header:"중간합계",Width:200,CanEdit:1,Color:"#DADADA"}, true );

// render 인자 false
for (var i = 0; i < 50; i++) {
  sheet.addCol( "EXT_SUBSUM" + i, 1, -1, {Type:"Int",Header:"중간합계",Width:200,CanEdit:1,Color:"#DADADA"}, true, false );
}

sheet.rerender();
```

### Read More
- [addRow method](./add-row)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.0.0.17|`render` 인자 추가|
