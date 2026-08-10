# selectCol ***(method)***

<!-- synonyms: selectCol, select-col, 열 선택, 컬럼 선택, 열 선택해제, 컬럼 지정, 컬럼 활성화, select, col, column, deselect -->

> 지정한 열을 선택 합니다.
>
> 시트 `Cfg`의 `SelectingCells`설정이 `0` 일때는 사용 하실 수 없습니다.

### Syntax
```javascript
boolean selectCol( col, select, valid, ignoreEvent );
```

### Parameters
|Name|Type|Required| Description |
|----------|-----|---|----|
|col|`string`|<span class='required'>필수</span>|선택할 열이름|
|select|`boolean`|<span class='optional'>선택</span>| 선택 / 선택해제  여부<br>`0(false)`:선택해제<br>`1(true)`:선택 (`default`)|
|valid|`boolean`|<span class='optional'>선택</span>|실제로 열 선택 가능여부 확인<br>(실제로 열 선택 되진 않고, 가능/불가능 여부를 확인해서 리턴)<br>`0(false)`:열 선택 가능여부 확인 안함 (`default`)<br>`1(true)`:열 선택 기능여부 확인 사용|
|ignoreEvent|`boolean`|<span class='optional'>선택</span>| [onSelectEnd](/docs/events/on-select-end) 이벤트 발생 여부 <br/>`0(false)`: 발생<br>`1(true)`: 발생하지 않음 (`default`)|

### Return Value
***boolean*** : 선택/선택해제 변경 여부

이미 선택한 열을 다시 선택하려 하거나, 해제된 행을 다시 해제하려 하면 `false`를 리턴

### Example
```javascript
//AMT,QTY 열을 선택
sheet.selectCol("AMT", 1);
sheet.selectCol("QTY", 1);
```

### Read More
- [clearSelection method](./clear-selection)
- [selectRow method](./select-row)
- [selectRange method](./select-range)
- [getSelectedRange method](./get-selected-range)
- [onSelectEnd event](/docs/events/on-select-end)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.3.0.14|`ignoreEvent` 인자 추가|
