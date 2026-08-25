# Menu ***(row)***

<!-- synonyms: row menu, context menu, right click menu, popup menu, row context menu, per-row menu, 컨텍스트 메뉴, 오른쪽 클릭 메뉴, 팝업 메뉴, 우클릭 메뉴, 행 메뉴, Menu 속성 -->

> 특정 행의 셀에서 마우스 우측 버튼 클릭 시 보여질 컨텍스트 메뉴를 설정합니다.


### Type
`mixed`( `object` \| `string` )

### Options
|Value|Description|
|-----|-----|
|`string`|첫 글자를 구분자로 사용하는 메뉴 문자열 (ex: `@저장@임시저장@취소` 또는 `*상신*취소`)|
|`object`|[Menu Object 설정 링크 참고](/docs/appx/menu)|

### Example
```javascript
//두 번째 헤더행(HR1)에만 마우스 우측 버튼 컨텍스트 메뉴 설정
sheet.getRowById("HR1")["Menu"] = "|엑셀다운로드|텍스트다운로드|PDF다운로드";

//조회 데이터에서 특정 행에만 컨텍스트 메뉴 적용
{"data":[
    {"Menu":"|상신하기|보류하기","ColName1":"Value1","ColName2":"Value2", ...}
]}

//선택한 항목은 onSelectMenu 이벤트에서 처리 (evtParam.result = 선택 항목, evtParam.row로 어느 행인지 구분)
options.Events = {
    onSelectMenu: function (evtParam) {
        switch (evtParam.result) {
            case "엑셀다운로드": evtParam.sheet.down2Excel(); break;
            case "상신하기":    /* 상신 처리 */ break;
            case "보류하기":    /* 보류 처리 */ break;
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
