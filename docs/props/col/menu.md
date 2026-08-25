# Menu ***(col)***

<!-- synonyms: 컨텍스트 메뉴, 우클릭 메뉴, 마우스 오른쪽 메뉴, 팝업 메뉴, menu, context menu, right click menu, popup menu -->

> 특정 열(컬럼)의 셀에서 마우스 우측 버튼 클릭 시 보여질 컨텍스트 메뉴를 설정합니다.


### Type
`mixed`( `object` \| `string` )

### Options
|Value|Description|
|-----|-----|
|`string`|첫 글자를 구분자로 사용하는 메뉴 문자열 (ex: `@저장@임시저장@취소` 또는 `*상신*취소`)|
|`object`|[Menu Object 설정 링크 참고](/docs/appx/menu)|

### Example
```javascript
//procs 열에서 마우스 우측 버튼 클릭 시 보여질 메뉴 설정
options.Cols = [
    ...
    {Type: "Text", Menu: "|진행|반려|전결|보류", Name: "procs", Width: 120 ...},
    ...
];

//선택한 항목은 onSelectMenu 이벤트에서 처리 (evtParam.col로 어느 열인지 구분)
options.Events = {
    onSelectMenu: function (evtParam) {
        if (evtParam.col === "procs") {
            // evtParam.result = 선택한 항목 (예: "진행")
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
