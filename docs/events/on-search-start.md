# onSearchStart ***(event)***

<!-- synonyms: 조회 시작, 검색 시작, 데이터 조회 전, 조회 취소, 대기 이미지 표시, 로딩 시작, on-search-start, search start, before search, search begin -->

> 조회 함수를 통한 데이터 조회가 시작하기 전에 발생합니다.  
> `1(true)` 값을 리턴 시 조회가 취소됩니다.  
> 메시지 표시 [(Cfg)SuppressMessage](/docs/props/cfg/suppress-message), 프로그레스바 [(Cfg)SearchProgress](/docs/props/cfg/search-progress)를 참고하세요.  
> 별도의 대기 이미지를 사용하려면 이 이벤트에서 표시하고 [onSearchFinish](/docs/events/on-search-finish)에서 제거하세요.

### Syntax

```
    onSearchStart : function(paramObject) {

    }
or
    sheet.bind("onSearchStart" , function(paramObject) {});
```

### Parameters
| Name | Type | Description |
|----------|-----|-------|
|sheet|`object`|시트 객체|
|type|`string`|조회/엑셀 여부(Search, EXCEL)|


### Return
***boolean***

### Example
```javascript
// 개별 시트에서 대기 이미지 처리
options.Events = {
    onSearchStart: function(evtParam) {
        //대기 이미지 표시 (jQuery BlockUI 사용 예시)
        $.blockUI();
    }
}

// ibsheet-common.js에서 공통 대기 이미지 처리 (jQuery BlockUI 사용 예시)
IBSheet.onBeforeCreate = function(obj) {
    var options = obj.options;
    options.Events = options.Events || {};

    // 기존 화면에 설정된 이벤트를 담아둠
    var origStart = options.Events.onSearchStart;
    // 공통 이벤트를 먼저 실행하고, 이후 화면단의 이벤트를 실행
    options.Events.onSearchStart = function(evtParam) {
        $.blockUI();
        if (origStart) return origStart(evtParam);
    };

    // 기존 화면에 설정된 이벤트를 담아둠
    var origFinish = options.Events.onSearchFinish;
    // 공통 이벤트를 먼저 실행하고, 이후 화면단의 이벤트를 실행
    options.Events.onSearchFinish = function(evtParam) {
        $.unblockUI();
        if (origFinish) origFinish(evtParam);
    };

    return obj;
};
```

### Read More
- [조회 이벤트 발생 순서](./02-search-event-flow)
- [SuppressMessage cfg](/docs/props/cfg/suppress-message)
- [onSearchFinish event](./on-search-finish)
- [doSearch method](/docs/funcs/core/do-search)
- [doSearchPaging method](/docs/funcs/core/do-search-paging)
- [loadSearchData method](/docs/funcs/core/load-search-data)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.24|기능 추가|
|core|8.0.0.26|`type` 추가|
