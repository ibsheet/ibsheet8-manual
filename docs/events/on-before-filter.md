# onBeforeFilter ***(event)***

<!-- synonyms: 필터링 전, 필터 적용 전, 필터 취소, doFilter 이전, on-before-filter, before filter, filter cancel -->

> 시트에서 필터링하기 전에 호출되는 이벤트입니다.  
> `1(true)`를 리턴시 필터링을 진행하지 않습니다.

### Syntax

```
    onBeforeFilter:function(paramObject) {

    }
or
    sheet.bind("onBeforeFilter" , function(paramObject) {});
```

### Parameters
| Name | Type | Description |
|----------|-----|------------|
|sheet|`object`|필터링이 적용될 시트 객체|
|type|`number`|필터링 동작 정보<br/>`0`:필터 값이 바뀐 경우<br/>`2`:렌더링 도중 필터링을 실행하거나 그룹의 변경이 필터링과 같이 발생한 경우|
<!--!
`[비공개 설명]` ***1이 있는데 이는 쿠키 관련된 것이므로 제외했고, 2번을 1번으로 바꾸어야할 것으로 보입니다.***
!-->


### Return
***boolean***  
`1(true)` 리턴 시 이후 필터링을 진행하지 않습니다.

### Example
```javascript
options.Events = {
    onBeforeFilter:function(evtParam){
        if(evtParam.type == 2) return false;
        return true;
    }
}
```

서버 페이징([SearchMode](/docs/props/cfg/search-mode) `3`/`4`/`5`)에서는 **시트 기본 필터(필터행 — [ShowFilter](/docs/props/cfg/show-filter) / [showFilterRow](/docs/funcs/core/show-filter-row))** 가 이미 조회된 페이지 데이터 안에서만 동작합니다.  
전체 데이터 기준으로 필터하려면, 아래처럼 기본 필터를 `return 1`로 막고 필터 조건을 [getFilter](/docs/funcs/core/get-filter)로 모아 [doSearchPaging](/docs/funcs/core/do-search-paging) 파라미터로 서버에 전송해 재조회합니다.

```javascript
options.Events = {
    onBeforeFilter: function (evtParam) {
        if (evtParam.type == 0) {                 // 필터 값이 바뀐 경우
            var sheet = evtParam.sheet;
            // 필터행에 걸린 모든 조건: [["col", "값", 연산자], ...]
            var filters = sheet.getFilter(0);
            // 모든 필터 컬럼을 검색 파라미터로 구성
            var filterParam = filters.map(function (f) {
                return f[0] + "=" + f[1];
            }).join("&");

            // doSearchPaging 호출 시 ibpage=1로 전송되어 필터 결과의 1페이지부터 조회됨
            sheet.doSearchPaging({ url: "/dofilter", param: filterParam });
            return 1;                             // 기본 필터 취소 → 서버 결과로 대체
        }
    }
}
```

### Read More
- [onAfterFilter event](./on-after-filter)
- [getFilter method](/docs/funcs/core/get-filter)
- [doSearchPaging method](/docs/funcs/core/do-search-paging)
- [SearchMode cfg](/docs/props/cfg/search-mode)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
