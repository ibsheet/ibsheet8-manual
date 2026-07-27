# setCheck ***(method)***

<!-- synonyms: 단일 체크 함수, 셀 체크, 체크 메서드, set check, 코드로 체크 -->

> `Bool` 타입 셀의 값을 체크/체크해제합니다.  
> 편집 불가능한 셀은 변경되지 않습니다. (편집 불가 셀까지 변경하려면 [setValue](./set-value)를 사용하세요)  
> `valid:1`로 호출하면 실제 변경 없이 변경 가능 여부만 반환합니다. (이미 같은 값/편집 불가/Bool 아닌 셀 등은 `false`)

### Syntax
```javascript
boolean setCheck( row, col, val, valid );
```

### Parameters
|Name|Type|Required| Description |
|----------|-----|---|----|
|row | `object` | <span class='required'>필수</span> | [데이터 로우 객체](/docs/appx/row-object)|
|col | `string` | <span class='required'>필수</span> | 열이름|
|val | `boolean` | <span class='optional'>선택</span> | 체크 여부<br>`0(false)`: 체크해제<br>`1(true)`: 체크<br>`null`: Toggle (`default`)|
|valid | `boolean` | <span class='optional'>선택</span> | 실제 변경 없이 변경 가능 여부만 확인<br>`0(false)`: 변경 수행 (`default`)<br>`1(true)`: 변경 가능 여부만 반환|

### Return Value
***boolean*** — 값이 변경되었으면 `true`, 변경되지 않았으면 `false`

### Example
```javascript
var r5 = sheet.getRowById("AR5");

// AR5의 "CHK" 셀 체크
sheet.setCheck(r5, "CHK", 1);

// 토글 (val 생략 시 현재 상태 반대로 변경)
sheet.setCheck(r5, "CHK");

// 변경 없이 가능 여부만 확인
var canChange = sheet.setCheck(r5, "CHK", 0, 1);
```

### Read More
- [setAllCheck method](./set-all-check)
- [setValue method](./set-value)
- [getRowsByChecked method](./get-rows-by-checked)
- [onBeforeChange event](/docs/events/on-before-change)
- [onAfterChange event](/docs/events/on-after-change)
- [check-event-flow](/docs/events/07-check-event-flow)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
