# onSearchFinish ***(event)***

<!-- synonyms: 조회완료, 조회 끝, 대기이미지 닫기, 로딩 제거, search complete, search finish, loading close -->

> [doSearch](/docs/funcs/core/do-search), [doSearchPaging](/docs/funcs/core/do-search-paging), [loadSearchData](/docs/funcs/core/load-search-data) 함수를 통해 로드된 데이터가 화면에 렌더링(표시)까지 완료된 상태에서 발생합니다.
>
> 조회가 실패한 경우(서버 에러, 타임아웃 등)에는 이 이벤트가 발생하지 않습니다.
>
> **<mark>주의</mark>** : 이 이벤트는 조회가 끝나고 화면에 떠 있는 대기이미지를 닫을 시 유용하며,  
> 시트에 접근하여 값 또는 속성을 바꾸는 작업을 할 경우 [onBeforeDataLoad](/docs/events/on-before-data-load)나 [onDataLoad](/docs/events/on-data-load) 이벤트가 적합합니다.

### Syntax

```
    onSearchFinish : function(paramObject) {

    }
or
    sheet.bind("onSearchFinish" , function(paramObject) {});
```

### Parameters

| Name | Type | Description |
|----------|-----|-------|
|sheet|`object`|시트 객체|
|type|`string`|조회/엑셀/텍스트 여부 (`Search`, `EXCEL`, `TEXT`)|

### Return
***none***

### Example
```javascript
// 대기 이미지 제거 (jQuery BlockUI 사용 예시)
// onSearchStart에서 표시한 대기 이미지를 렌더링 완료 후 닫습니다.
options.Events = {
    onSearchFinish:function(evtParam){
        $.unblockUI();
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

    // 조회 실패 시 onSearchFinish가 발생하지 않으므로
    // onBeforeDataLoad에서 data가 없으면 대기이미지를 닫는다.
    var origBeforeDataLoad = options.Events.onBeforeDataLoad;
    options.Events.onBeforeDataLoad = function(evtParam) {
        if (!evtParam.data) $.unblockUI();
        if (origBeforeDataLoad) origBeforeDataLoad(evtParam);
    };

    var origFinish = options.Events.onSearchFinish;
    options.Events.onSearchFinish = function(evtParam) {
        $.unblockUI();
        if (origFinish) origFinish(evtParam);
    };

    return obj;
};
```

### Read More
- [조회 이벤트 발생 순서](/docs/events/02-search-event-flow)
- [onReceiveData event](/docs/events/on-receive-data)
- [onBeforeDataLoad event](./on-before-data-load)
- [onDataLoad event](./on-data-load)
- [onSearchStart event](./on-search-start)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.0.0.26|`type` 추가|
