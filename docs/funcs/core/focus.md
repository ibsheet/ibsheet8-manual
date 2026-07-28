# focus ***(method)***

<!-- synonyms: 포커스, 셀 포커스, 셀 이동, focus, 셀 선택 -->

> 지정한 특정 셀에 포커스를 줍니다.  
> `row`, `col` 중 적어도 하나는 지정해야 합니다 (둘 다 생략 시 `null` 반환).  
> 시트 외부에 버튼을 클릭함으로써 포커스를 설정하고자 하는 경우에는 `setTimeout`을 통해 딜레이를 주어야 합니다.

### Syntax
```javascript
boolean focus( row, col, pagepos, ignoreEvent, triggerOnFocus, skipSheetFocus );
```

### Parameters
|Name|Type|Required|Description|
|----------|-----|---|----|
|row|`object`|<span class='optional'>선택</span>|[데이터 로우 객체](/docs/appx/row-object)<br/>생략 또는 `""`, `null` 전달 시 현재 포커스된 행 사용 (포커스된 행이 없으면 보이는 첫 행)|
|col|`string`|<span class='optional'>선택</span>|열이름<br/>생략 또는 `""`, `null` 전달 시 행의 첫 번째 컬럼 사용|
|pagepos|`number`|<span class='optional'>선택</span>|서버페이징 사용시 페이지 지정 (`default: null`)|
|ignoreEvent|`boolean`|<span class='optional'>선택</span>|함수 호출시 `focus Event(onBeforeFocus, onFocus)`를 발생시킬지 유무<br>`0(false)`:`focus Event` 발생 시킴 (`default`)<br>`1(true)`:`focus Event`를 발생 시키지 않음|
|triggerOnFocus|`boolean`|<span class='optional'>선택</span>|이미 선택한 셀을 다시 선택하는 함수 호출시 `focus Event(onBeforeFocus, onFocus)`를 항상 발생시킵니다.<br>`0(false)`:이미 선택된 셀을 함수로 다시 포커스 하였을 때, `focus Event`를 발생 시키지 않음 (`default`)<br>`1(true)`:이미 선택된 셀을 함수로 다시 포커스 하였을 때, `focus Event` 를 발생 시킴|
|skipSheetFocus|`boolean`|<span class='optional'>선택</span>|셀 포커스는 이동하되 시트 자체에는 포커스를 주지 않을지 여부<br/>외부 input 등에서 포커스를 유지한 채 시트 내부 셀만 이동하고자 할 때 사용합니다. [IgnoreFocused](/docs/props/cfg/ignore-focused) `2`와 유사한 동작입니다.<br>`0(false)`:시트에 포커스 적용 (`default`)<br>`1(true)`:시트 자체 포커스는 생략, 셀 포커스만 이동|

### Return Value
***boolean*** : 포커스가 지정되면 true, 이미 포커스가 된 셀에 함수 적용시 false, 해당셀이 없는 경우 null 리턴

### Example
```javascript
// 특정 행/열로 포커스
sheet.focus(sheet.getRowById("AR5"), "CARNO");

// 현재 포커스 행의 title 셀 (포커스가 없으면 보이는 첫 행의 title 셀)
sheet.focus("", "title");

// 특정 행의 첫 번째 셀로 (col 생략)
sheet.focus(sheet.getRowById("AR5"), "");

// 시트 외부 버튼 클릭에서 호출 시 setTimeout으로 딜레이 주는 패턴
document.getElementById("btn_validCheck").onclick = function() {
    setTimeout(function() {
        var errRow = sheet.getRowById("AR4");
        sheet.focus(errRow, "CARNO");
    }, 10);
};

// 외부 input의 포커스를 유지한 채 시트 셀 포커스만 이동
document.getElementById("searchInput").oninput = function() {
    var row = sheet.getRowById("AR5");
    sheet.focus(row, "CARNO", null, 0, 0, 1); // skipSheetFocus:1
};
```

### Read More
- [blur method](./blur)
- [startEdit method](./start-edit)
- [IgnoreFocused cfg](/docs/props/cfg/ignore-focused)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.0.0.7|`ignoreEvent` 인자 추가|
|core|8.1.0.94|`triggerOnFocus` 인자 추가|
|core|8.4.0.4|`skipSheetFocus` 인자 추가|
