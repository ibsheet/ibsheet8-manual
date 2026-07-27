# setIconCheck ***(method)***

<!-- synonyms: 아이콘 체크 함수, Icon Check 변경, 좌측 체크박스 변경, set icon check -->

> [Icon](/docs/props/col/icon)이나 [Button](/docs/props/col/button) 속성을 `"Check"`로 설정해 만든 셀의 별도 체크박스 값을 변경합니다.  
> Bool 타입의 본체 체크박스가 아니라 [Checked](/docs/props/cell/checked)로 다루는 좌/우측 체크박스를 대상으로 합니다.  
> 변경된 체크 상태는 [getSaveJson](/docs/funcs/core/get-save-json) 등 저장 함수의 결과에 포함되지 않습니다.

### Syntax
```javascript
void setIconCheck( row, col, val );
```

### Parameters
|Name|Type|Required| Description |
|----------|-----|---|----|
|row | `object` | <span class='required'>필수</span> | [데이터 로우 객체](/docs/appx/row-object)|
|col | `string` | <span class='required'>필수</span> | 열이름|
|val | `boolean` | <span class='optional'>선택</span> | 체크 여부<br>`0(false)`: 체크해제<br>`1(true)`: 체크<br>`null`: Toggle (`default`)|

### Return Value
***none***

### Example
```javascript
// 포커스 셀의 Icon Check 값을 체크해제로 변경
sheet.setIconCheck(sheet.getFocusedRow(), sheet.getFocusedCol(), 0);
```

### Read More
- [Icon col](/docs/props/col/icon)
- [Button col](/docs/props/col/button)
- [Checked cell](/docs/props/cell/checked)
- [onIconClick event](/docs/events/on-icon-click)
- [setCheck method](./set-check)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
