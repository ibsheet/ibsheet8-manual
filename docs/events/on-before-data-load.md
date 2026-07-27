# onBeforeDataLoad ***(event)***
> 데이터가 시트에 로드되기 전에 발생하는 이벤트입니다.
>
> 데이터가 시트 내부에서 파싱되기 전 단계이므로 **row 객체가 생성되지 않아** row 객체를 인자로 사용하는 함수는 사용할 수 없습니다.  
> 이 시점에서는 이벤트 파라미터인 `data` 객체를 활용하여 데이터를 가공할 수 있습니다.
>
> 파싱이 완료된 이후에는 [onDataLoad](./on-data-load)이벤트가 발생합니다.

### Syntax

```
    onBeforeDataLoad:function(paramObject) {

    }
or
    sheet.bind("onBeforeDataLoad" , function(paramObject) {});
```

### Parameters


| Name | Type | Description |
|----------|-----|------------|
|sheet|`object`|데이터를 로딩할 시트 객체|
|result|`number`| 1. 서버를 통한 조회 시([doSearch](/docs/funcs/core/do-search))<br/>`0`:성공<br/>`-1`:빈 URL (`예: sheet.doSearch("")`)<br/>`-3`:요청 Url이 잘못된 경우나 네트워크 오류 등으로 결과를 받지 못한 경우<br/>`-5`:응답 결과가 빈값인 경우<br/>`-6`:연결 시간 초과((cfg)Timeout 초과)<br/>`-7`:잘못된 데이터 형식(대부분 데이터 이상)<br/>`이외`:사용자 정의 코드<br/><br/> 2. 일반 데이터 조회 시([loadSearchData](/docs/funcs/core/load-search-data))<br/>`0`:성공<br/>`-7`:잘못된 데이터 형식<br/>|
|data|`object`|시트에 로딩될 데이터|
|message|`string`|조회 결과 `json`에 포함된 `Message` 내용|
|response|`object`|`response` 객체|

### Return
***none***

### Example
```javascript
// 조회 후 오류에 대한 예시
options.Events = {
    onBeforeDataLoad:function(evtParam){
        if (evtParam.result === -100) {
            alert("세션이 종료되었습니다.\n로그인 화면으로 이동합니다.");
            location.href = "/login.do";
        } else if (evtParam.result < 0) {
            alert("조회 중 오류가 발생하였습니다.\n" + evtParam.message);
        }
    }
}


// 조회된 내용에 대한 수정 예시
options.Events = {
    onBeforeDataLoad:function(evtParam){
        // 조회 결과 데이터
        var DATA = evtParam.data;
        // 조회된 데이터 일부를 수정한다.
        for(var i = 0; i < DATA.length; i++){
            var row = DATA[i];
            // AttrYn 컬럼에 값이 Y 인 경우 ConfirmFinish 컬럼에 "결정완료"를 설정하고
            // 해당 행의 Edit를 막는다. (data 객체를 직접 수정하면 시트에 반영되므로 별도 리턴은 필요 없음)
            if(row["AttrYn"] == "Y"){
                row["ConfirmFinish"] = "결정완료";
                row["CanEdit"] = 0;
            }
            // 셀 단위 속성 설정 (컬럼명 + 속성명)
            if(row["price"] >= 10000000){
                row["priceTextColor"] = "#FF0000";  // price 셀의 글자색을 빨간색으로 설정
            }
        }
    }
}
```

```javascript
// ibsheet-common.js에서 공통 오류 처리 (공통 이벤트 처리 방법 참고)
IBSheet.onBeforeCreate = function(obj) {
    var options = obj.options;
    options.Events = options.Events || {};

    // 기존 화면에 설정된 이벤트를 담아둠
    var origEvent = options.Events.onBeforeDataLoad;
    // 공통 이벤트를 먼저 실행하고, 이후 화면단의 이벤트를 실행
    options.Events.onBeforeDataLoad = function(evtParam) {
        // 공통 오류 처리
        if (evtParam.result === -100) {
            alert("세션이 종료되었습니다.");
            location.href = "/login.do";
            return;
        } else if (evtParam.result < 0) {
            alert("오류가 발생하였습니다.\n" + evtParam.message);
            return;
        }
        // 개별 페이지 이벤트 호출
        if (origEvent) return origEvent(evtParam);
    };

    return obj;
};
```

```javascript
// 조회 결과 json 참고
{
    //IO,Result,Message 대소문자 주의!
    "IO":{"Result":100,"Message":"정상조회완료"},
    "Data":[ ... ]
}
```

### Read More

- [조회 이벤트 발생 순서](/docs/events/02-search-event-flow)
- [조회 응답 규격](/docs/dataStructure/data-structure)
- [페이징 응답 규격](/docs/dataStructure/paging-structure)
- [doSearch method](/docs/funcs/core/do-search)
- [doSearchPaging method](/docs/funcs/core/do-search-paging)
- [loadSearchData method](/docs/funcs/core/load-search-data)
- [onReceiveData event](/docs/events/on-receive-data)
- [onDataLoad event](/docs/events/on-data-load)
- [공통 이벤트 처리 방법](/docs/appx/shared-event)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
