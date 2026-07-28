# blur ***(method)***

<!-- synonyms: 포커스 해제, 시트 포커스 해제, 셀 포커스 해제, blur, 포커스 끄기 -->

> 시트의 포커스를 해제합니다.  
> 시트에서 버튼을 통해 layer 팝업을 띄우는 경우, 시트의 포커스를 해제해야만 layer 팝업 내에서 원활하게 포커스를 이동할 수 있습니다.

### Syntax
```javascript
boolean blur( mode );
```

### Parameters
|Name|Type|Required|Description|
|----------|-----|---|----|
|mode|`number`|<span class='optional'>선택</span>|해제 범위 설정 (Options 참고)|

### Options
|Value|Description|
|-----|-----|
|`0`|포커스 레이어 + 시트 영역 포커스 모두 해제 (`default`) — Tab/방향키 입력 시 시트 무반응|
|`1`|포커스 레이어만 해제 — Tab/방향키 입력 시 시트가 다시 셀 포커스를 잡음|
|`2`|포커스 레이어만 유지 — Tab/방향키 입력 시 시트 무반응|

### Return Value
***boolean*** : 정상적으로 포커스가 해제된 경우 `true`, 포커스 해제에 실패한 경우 `false`를 리턴

### Example
```javascript
// layer 팝업 오픈 전에 포커스 레이어만 유지
sheet.blur(2);
dialog.dialog("open");
```

### Read More
- [focus method](./focus)
- [onFocus event](/docs/events/on-focus)
- [IgnoreFocused cfg](/docs/props/cfg/ignore-focused)
- [CanFocus col](/docs/props/col/can-focus)
- [CanFocus row](/docs/props/row/can-focus)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
