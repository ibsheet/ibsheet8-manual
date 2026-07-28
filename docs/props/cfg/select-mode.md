# SelectMode ***(cfg)***

> 마우스로 행 또는 셀을 선택(`Selection`)할 때,
> 선택 영역의 갱신 방식과 `Focus`(현재 커서 위치) 이동 동작을 설정합니다.
> 영역 선택 도중 `Focus`가 자동으로 이동할 때 `onBeforeFocus` / `onFocus` 이벤트를 발생시키려면 `3` 또는 `4`로 설정해야 합니다.

<!-- synonyms: select mode, selection mode, selection behavior, shift select, shift range selection, ctrl select, range selection mode, focus and selection, selection toggle, additive selection, 선택 모드, 선택 방식, 범위 선택, Shift 선택, 선택 누적, 포커스 이동 -->

<!--!
  * `[비공개 설명]` SelectMode: 0 (기존)은 shift + 드래그 시 SelectingCells: 0이 아닐 때만 선택을 해제  
!-->
### Type
`number`

### Options
|Value|Description|
|-----|-----|
| `0` | `Ctrl + 클릭` 또는 `마우스 드래그`로 선택하더라도 `Focus` 행은 변경되지 않습니다. (`default`)<br/><br/>- 선택된 범위에 `Focus` 행이 포함된 상태에서 `Shift + 클릭`으로 범위를 다시 지정하면,<br/> `Focus` 행을 기준으로 해당 범위는 토글 처리됩니다.|
| `1` | `Ctrl + 클릭` 또는 `마우스 드래그`로 선택하면 `Focus`는 선택 영역의 첫 번째 행으로 이동합니다.<br/><br/>- `Shift + 클릭` 시 현재 `Focus`(커서) 행부터 클릭한 행까지 범위를 선택합니다.<br/>- 기존 선택은 유지되지 않고 새 범위로 변경됩니다. |
| `2` | `Ctrl + 클릭` 또는 `마우스 드래그`로 선택하면 `Focus`는 선택 영역의 첫 번째 행으로 이동합니다.<br/><br/>- `Shift + 클릭` 시 기존 선택을 유지하면서 새로운 선택 범위를 추가합니다. |
| `3` | `1`번 동작과 동일하며, 영역 선택으로 `Focus`가 이동할 때 `Focus` 관련 이벤트가 발생합니다. |
| `4` | `2`번 동작과 동일하며, 영역 선택으로 `Focus`가 이동할 때 `Focus` 관련 이벤트가 발생합니다. |

### Example
```javascript
options.Cfg = {
   SelectMode: 1
};

options.Cfg = {
  SelectingCells: 0,  // 행 단위 선택
  SelectMode: 1       // 선택 시 Focus 이동 + Shift 범위 선택
};
```

### Read More

- [SelectingCells cfg](./selecting-cells)


### Since

|product|version|desc|
|---|---|---|
|core|8.3.0.28|기능 추가|
|core|8.4.0.2|3, 4 옵션 추가|