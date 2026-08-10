# onDataLoad ***(event)***

<!-- synonyms: 데이터 로드, 데이터 적재 완료, 데이터 파싱 후, on-data-load, data load, data loaded, load complete -->

> 데이터가 시트 내에서 파싱되어 로드된 후에 발생합니다.  
> 내부적인 로딩은 완료되었지만 화면에 반영(렌더링)은 일어나기 전 단계입니다.  
> 이 시점에는 **row 객체가 생성된 상태**이므로, **row 객체**를 인자로 사용하는 함수들을 사용할 수 있습니다.

### Syntax

```
    onDataLoad : function(paramObject) {

    }
or
    sheet.bind("onDataLoad" , function(paramObject) {});
```

### Parameters
| Name | Type | Description |
|----------|-----|-------|
|sheet|`object`|데이터가 로드된 시트 객체|
|result|`number`| 1. 서버를 통한 조회 시([doSearch](/docs/funcs/core/do-search))<br/>`0`:성공<br/>`-1`:빈 URL (`예: sheet.doSearch("")`)<br/>`-3`:요청 Url이 잘못된 경우나 네트워크 오류 등으로 결과를 받지 못한 경우<br/>`-5`:응답 결과가 빈값인 경우<br/>`-6`:연결 시간 초과((cfg)Timeout 초과)<br/>`-7`:잘못된 데이터 형식(대부분 데이터 이상)<br/>`이외`:사용자 정의 코드<br><br/> 2. 일반 데이터 조회 시([loadSearchData](/docs/funcs/core/load-search-data))<br/>`0`:성공<br/>`-7`:잘못된 데이터 형식<br/>|
|message|`string`|조회 결과 `json`에 포함된 `Message` 내용|
|response|`object`|`response` 객체|
|type|`string`|조회/엑셀/텍스트 여부 (`Search`, `EXCEL`, `TEXT`)|

<!--!
### Return
`[비공개]` ***boolean***
!-->

### Example
```javascript
// row 객체가 생성된 상태이므로 행별 처리 가능
// 이후 자동으로 렌더링이 되므로 render:0으로 설정
options.Events = {
    onDataLoad:function(evtParam){
        if (evtParam.result == 0) {
            var rows = evtParam.sheet.getDataRows();
            for (var i = 0; i < rows.length; i++) {
                if (rows[i].status === "완료") {
                    // 완료 행의 배경색을 회색으로 설정
                    evtParam.sheet.setAttribute(rows[i], "", "Color", "#CCCCCC", 0);
                }
            }
        }
    }
}

// 셀 단위 속성 설정
options.Events = {
    onDataLoad:function(evtParam){
        if (evtParam.result == 0) {
            var rows = evtParam.sheet.getDataRows();
            for (var i = 0; i < rows.length; i++) {
                // 금액이 1000만 이상인 셀의 글자색을 빨간색으로 설정
                if (rows[i].price >= 10000000) {
                    evtParam.sheet.setAttribute(rows[i], "price", "TextColor", "#FF0000", 0);
                }
            }
        }
    }
}
```
### Read More
- [조회 응답 규격](/docs/dataStructure/data-structure)
- [조회 이벤트 발생 순서](/docs/events/02-search-event-flow)
- [doSearch method](/docs/funcs/core/do-search)
- [doSearchPaging method](/docs/funcs/core/do-search-paging)
- [loadSearchData method](/docs/funcs/core/load-search-data)
- [onReceiveData event](/docs/events/on-receive-data)
- [onBeforeDataLoad event](/docs/events/on-before-data-load)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.0.0.26|`type` 추가|
