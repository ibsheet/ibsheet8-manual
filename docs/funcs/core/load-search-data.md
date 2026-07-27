# loadSearchData ***(method)***

<!-- synonyms: 조회, 데이터 조회, 데이터 바인딩, 대기이미지, 로딩, search, data bind, data load, loading -->

> JSON형식의 데이터를 시트에 바인딩합니다. AJAX 통신 없이 데이터만 로드합니다.  
> [SearchMode](/docs/props/cfg/search-mode) 0, 1, 2에서 사용합니다.  
> AJAX 통신이 필요한 경우 [doSearch](/docs/funcs/core/do-search)를 사용하세요.  
> 비동기형식으로 동작하므로, 데이터 로드 후 처리는 [onReceiveData](/docs/events/on-receive-data), [onBeforeDataLoad](/docs/events/on-before-data-load), [onDataLoad](/docs/events/on-data-load) 이벤트에서 구현해야 합니다.  
> 기본적으로 `loadSearchData`는 시트의 기존 데이터를 제거하고 데이터를 로드합니다.  
> 기존 데이터 뒤에 새 데이터를 추가하려면 `append: true` 옵션을 사용하세요.  
> JSON 데이터 구조와 관련된 상세 내용은 [조회 응답 규격](/docs/dataStructure/data-structure)을 참고하세요.  
> 조회 시 자동 포커스 [(Cfg)IgnoreFocused](/docs/props/cfg/ignore-focused), 메시지 표시 [(Cfg)SuppressMessage](/docs/props/cfg/suppress-message), 프로그레스바 [(Cfg)SearchProgress](/docs/props/cfg/search-progress)를 참고하세요.

### Syntax

```javascript
void loadSearchData( data, append, callback, sync, next, strictParse, parent, ignoreEvent );
```

### Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| data | `string` \| `object` \| `array` | <span dir="">필수</span> | JSON형식의 데이터<br/>`{Data:[{...}]}`, `'{Data:[{...}]}'`, `[{...}]` 형태 모두 가능 |
| append | `boolean` | <span dir="">선택</span> | 기존 데이터 하단에 `append` 여부<br>조회 방식의 차이로 인해 `append:1(true)`사용 시 [SearchMode](/docs/props/cfg/search-mode):2인 경우 [onRenderFinish](/docs/events/on-render-finish)이벤트가 발생하지 않습니다.<br>`0(false)`:기존 데이터 제거 후 조회 데이터 로드 (`default`)<br>`1(true)`:기존 데이터에 조회 데이터 추가|
| callback | `function` | <span dir="">선택</span> | 조회 후 호출할 콜백 함수<br>ex) `sheet`: 시트 객체, `data`: 조회 데이터, `result(0)`: 조회 성공 |
| sync | `boolean` | <span dir="">선택</span> | 동기 조회 여부. <br>`0(false)`: 비동기 방식 (`default`)<br>`1(true)`: 동기 방식 |
| next | `object` | <span dir="">선택</span> | [데이터 로우 객체](/docs/appx/row-object)<br>지정한 행 위에 데이터가 추가됨. (`append:1(true)`일때만 사용 가능) |
| strictParse | `boolean` | <span dir="">선택</span> | JSON 파서 선택<br>`0(false)`:유연한 파서 사용 (`default`) — 여분의 콤마, 프로퍼티 이름 쌍따옴표 생략 허용<br>`1(true)`:브라우저 JSON.parse() 사용 (약 5배 빠르나 5만건 이내에서는 차이 미미)|
| parent | `object` | <span dir="">선택</span> | [데이터 로우 객체](/docs/appx/row-object)<br>(동적 트리 조회 사용시 부모에 해당하는 행 지정) |
| ignoreEvent | `boolean` | 선택 | 조회 관련 이벤트를 발생시키지 않도록 하는 인자 <br>`0(false)`:조회 관련 이벤트를 발생 시킴 (`default`)<br>`1(true)`:조회 관련 이벤트를 발생 시키지 않음 |

### Return Value

**_none_**

### Example

```javascript
var DATA = {"Data":[
    {"EMP_ID":"08212","EMP_NM":"홍길동","DEPT_CD":"031"},
    {"EMP_ID":"07417","EMP_NM":"허균","DEPT_CD":"120"},
    {"EMP_ID":"02600","EMP_NM":"홍판서","DEPT_CD":"405"},
]};

// 기본 조회 — 기존 데이터를 제거하고 로드
sheet.loadSearchData(DATA);

// 기존 데이터 밑에 데이터를 append
sheet.loadSearchData(DATA, 1);

// 지정한 행 위에 데이터가 추가됨
sheet.loadSearchData({ data: DATA, append: true, next: sheet.getRowByIndex(3) })

// Level 기반 트리 데이터를 Items 구조로 변환하여 로드
// 최상위 노드는 0, 하위 노드는 부모보다 1씩 증가
var treeData = {
    "Data":[
        {Level:0, sProduct:"내부 시스템 개발 사업", sKind:"프로젝트", sPrice:"29"},
        {Level:1, sProduct:"글로벌 통합 인사시스템", sKind:"프로젝트", sPrice:"192"},
        {Level:2, sProduct:"물산 E-HR시스템", sKind:"기타", sPrice:"4"},
        {Level:2, sProduct:"제조 E-HR시스템", sKind:"기타", sPrice:"4"},
    ]
};
var convertData = IBSheet.v7.convertTreeData(treeData);
sheet.loadSearchData(convertData);
```

```javascript
// 대기 이미지 처리 (jQuery BlockUI 사용 예시)
// 대기 이미지는 렌더링 완료 후 onSearchFinish에서 닫는 것을 권장합니다.
$.ajax({
    url: "./insaAppMain.do",
    method: "POST",
    data: { dept_cd: "031" },
    beforeSend: function() {
        $.blockUI();
    },
    success: function(data) {
        sheet.loadSearchData(data);
        // $.unblockUI(); // 여기서 닫으면 시트에 데이터가 렌더링 되기 전에 닫힘
    },
    error: function() {
        alert("조회에 실패했습니다.");
        $.unblockUI();
    }
});

// 렌더링 완료 후 대기 이미지 닫기
options.Events = {
    onSearchFinish: function(evtParam) {
        $.unblockUI();
    }
}
```

### Read More

- [SearchMode cfg](/docs/props/cfg/search-mode)
- [조회 이벤트 발생 순서](/docs/events/02-search-event-flow)
- [조회 응답 규격](/docs/dataStructure/data-structure)
- [트리 응답 규격](/docs/dataStructure/tree-structure)
- [doSearch method](./do-search)
- [doSearchPaging method](./do-search-paging)
- [onBeforeDataLoad](/docs/events/on-before-data-load)
- [onDataLoad event](/docs/events/on-data-load)
- [onReceiveData event](/docs/events/on-receive-data)
- [SuppressMessage cfg](/docs/props/cfg/suppress-message)
- [SearchProgress cfg](/docs/props/cfg/search-progress)

### Since

| product | version | desc |
|---------|---------|------|
| core | 8.0.0.0 | 기능 추가 |
| core | 8.0.0.6 | `sync` 인자 추가 |
| core | 8.0.0.7 | `next`, `strictParse` 인자 추가 |
| core | 8.0.0.25 | `parent` 인자 추가 |

