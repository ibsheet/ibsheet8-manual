# Menu ***(cfg)***

<!-- synonyms: Menu, cfg menu, context menu, right click menu, sheet menu, contextmenu, 컨텍스트 메뉴, 우클릭 메뉴, 오른쪽 클릭 메뉴, 시트 메뉴, 컨텍스트, 마우스 우측 메뉴, 우측 버튼 메뉴 -->

> 마우스 우측 버튼 클릭 시 보여질 컨텍스트 메뉴를 설정합니다.  
> `InfoRow`를 제외한 시트의 다른 행들에서 표시됩니다.

### Type
`mixed`( `object` \| `string` )

### Options
|Value|Description|
|-----|-----|
|`string`|첫 글자를 구분자로 사용하는 메뉴 문자열 (ex: `@저장@임시저장@취소` 또는 `*상신*취소`)|
|`object`|[Menu Object 설정 링크 참고](/docs/appx/menu)|

### Example
```javascript
options.Cfg = { Menu: "|행추가|행숨기기|행삭제" };

//선택한 항목은 onSelectMenu 이벤트에서 처리 (evtParam.result = 선택 항목)
options.Events = {
    onSelectMenu: function (evtParam) {
        switch (evtParam.result) {
            case "행추가":   evtParam.sheet.addRow();               break;
            case "행숨기기": /* 행 숨김 처리 */                     break;
            case "행삭제":   evtParam.sheet.removeRow(evtParam.row); break;
        }
    }
};
```

### Read More
- [Menu appendix](/docs/appx/menu)
- [onSelectMenu event](/docs/events/on-select-menu)
- [onShowMenu event](/docs/events/on-show-menu)
- [MenuHSeparator cfg](/docs/props/cfg/menu-h-separator)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
