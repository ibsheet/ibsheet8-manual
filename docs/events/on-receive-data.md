# onReceiveData ***(event)***

<!-- synonyms: 데이터 수신, 조회 응답 수신, 서버 응답 받음, on-receive-data, receive data, data received, ajax response -->

> 데이터 조회 시([doSearch](/docs/funcs/core/do-search), [doSearchPaging](/docs/funcs/core/do-search-paging), [loadSearchData](/docs/funcs/core/load-search-data)), 시트가 데이터를 받은 직후 발생하는 이벤트입니다.
>
> [onBeforeDataLoad](/docs/events/on-before-data-load) 이벤트 보다 먼저 발생합니다.
>
> `true(1)`를 리턴하면 이후 데이터 파싱 작업과 관련 이벤트가 모두 중단됩니다.

### Syntax

```
    onReceiveData:function(paramObject) {

    }
or
    sheet.bind("onReceiveData" , function(paramObject) {});
```

### Parameters


| Name | Type | Description |
|----------|-----|------------|
|sheet|`object`|데이터를 로딩할 시트 객체|
|data|`mixed`( `string` \| `object` )|조회된 데이터<br/>서버 응답(`loadSearchData`는 넘긴 값)이 문자열이면 `string`, 객체면 `object`로 전달됩니다.<br/>엑셀 업로드(`type`이 `EXCEL`) 시에는 행 데이터 배열로 전달됩니다.|
|response|`object`|`response` 객체|
|type|`string`|조회/엑셀/텍스트 여부 (`Search`, `EXCEL`, `TEXT`)|

### Return
***mixed( `object` \| `boolean` )***

|리턴값|동작|
|---|---|
|없음|받은 데이터를 그대로 시트에 로딩합니다.|
|`object`|받은 데이터 대신 리턴한 데이터를 시트에 로딩합니다.|
|`true(1)`|이후 데이터 파싱과 관련 이벤트를 중단합니다.|

> 리턴하는 데이터의 구조는 호출한 함수에 따라 다릅니다.  
> doSearch는 `Data`가 있어야 합니다: `{Data: [{...}, {...}]}`  
> doSearchPaging은 `Total`도 있어야 합니다: `{Total: 건수, Data: [{...}]}`  
> loadSearchData는 배열 `[{...}, {...}]`만 리턴해도 됩니다.  
> 엑셀 업로드(`type`이 `EXCEL`)도 배열 `[{...}, {...}]`만 리턴해도 됩니다.  
> 트리 구조는 [트리 응답 규격](/docs/dataStructure/tree-structure)을 참고하세요.  
> 상세 내용은 [조회 응답 규격](/docs/dataStructure/data-structure), [페이징 응답 규격](/docs/dataStructure/paging-structure)을 참고하세요.

### Example
```js
// 조회된 내용에 대한 수정 예시
options.Events = {
    onReceiveData: function(evtParam) {
        var DATA = evtParam.data; // 조회 결과 데이터
        var parseData = typeof DATA === "string" ? JSON.parse(DATA) : DATA; // string이면 parsing

        // 조회된 데이터 일부를 수정한다
        /**
         * 조회 데이터 구조
         * { data: [{}, {}], etc: []}
         */
        for (var i = 0; i < parseData.data.length; i++){
            var row = parseData.data[i];
            // AttrYn 컬럼에 값이 Y 인 경우 ConfirmFinish 컬럼에 "결정완료"를 설정
            if (row["AttrYn"] == "Y") {
                row["ConfirmFinish"] = "결정완료";
                row["CanEdit"] = 0;
            }
        }

        return parseData; // 파싱 후 수정된 데이터 return
    }
}

// 외부 API(공공데이터 등) 응답을 IBSheet 데이터 구조로 변환하는 예시
// doSearchPaging은 AJAX가 내장되어 있으므로 서버 응답을 가공할 수 있는 시점은 이 이벤트뿐입니다.
options.Events = {
    onReceiveData: function(evtParam) {
        var data = evtParam.data;
        var response = typeof data === "string" ? JSON.parse(data) : data;
        // 외부 API 응답 구조를 IBSheet 구조로 변환
        var result = {
            Data: response.items.map(function(item) {
                return {
                    name: item.serviceName,
                    code: item.serviceCode,
                    status: item.activeYn
                };
            }),
            Total: response.totalCount
        };
        return result;
    }
}

// doSearch로 트리 조회 시 Level 기반 데이터를 Items 구조로 변환
// doSearch는 AJAX가 내장되어 있으므로 변환할 수 있는 시점은 이 이벤트뿐입니다.
options.Events = {
    onReceiveData: function(evtParam) {
        var data = evtParam.data;
        if (typeof data === "string") data = JSON.parse(data);
        return IBSheet.v7.convertTreeData(data);
    }
}
```

### Read More

- [조회 이벤트 발생 순서](/docs/events/02-search-event-flow)
- [doSearch method](/docs/funcs/core/do-search)
- [doSearchPaging method](/docs/funcs/core/do-search-paging)
- [loadSearchData method](/docs/funcs/core/load-search-data)
- [onDataLoad event](./on-data-load)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.19|기능 추가|
|core|8.0.0.24|`loadSearchData` 사용시에도 이벤트 발생하도록 추가|
|core|8.0.0.26|`type` 추가|
|core|8.1.0.73|데이터 파싱 중단 기능 추가|
