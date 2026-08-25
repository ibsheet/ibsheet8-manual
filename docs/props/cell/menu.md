# Menu ***(cell)***

<!-- synonyms: Menu, 셀 메뉴, 컨텍스트 메뉴, 우클릭 메뉴, 팝업 메뉴, 오른쪽 클릭 메뉴, 셀 우클릭 메뉴, cell menu, context menu, right-click menu, popup menu -->

> 특정 셀 위에서 마우스 우측 버튼 클릭 시 보여질 컨텍스트 메뉴를 설정합니다.

### Type
`mixed`( `object` \| `string` )

### Options
|Value|Description|
|-----|-----|
|`string`|첫 글자를 구분자로 사용하는 메뉴 문자열 (ex: `@저장@임시저장@취소` 또는 `*상신*취소`)|
|`object`|[Menu Object 설정 링크 참고](/docs/appx/menu)|

### Example
```javascript
//1. 메소드를 통해 특정 셀에 속성 적용 (열이름: CLS)
sheet.setAttribute(sheet.getRowById("AR99"), "CLS", "Menu", "|진행|취소");


//2. 객체에 직접 접근해서 속성 적용 (열이름: CLS)
var ROW = sheet.getRowById("AR10");
ROW["CLSMenu"] = "|보류|결제|전결";
//변경내용 확인
sheet.refreshCell({row:ROW, col:"CLS"});


//3. 조회 데이터 내에서 속성 적용  (열이름: CLS)
{
    data:[
        {... , "CLSMenu":"|국내|해외" , ...}
    ]
}

//4. 선택한 항목은 onSelectMenu 이벤트에서 처리 (evtParam.col로 어느 셀인지 구분)
options.Events = {
    onSelectMenu: function (evtParam) {
        if (evtParam.col === "CLS") {
            // evtParam.result = 선택한 항목 (예: "진행")
            // 선택값에 따른 처리
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
