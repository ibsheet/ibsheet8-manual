# doSearchPaging ***(method)***

<!-- synonyms: 페이징 조회, 서버 페이징, 대기이미지, 로딩, paging, server paging, loading -->

> 페이징 조회 (cfg [SearchMode](/docs/props/cfg/search-mode) : `3` or `4` or `5`) 전용 메서드입니다.  
> 조회 데이터 JSON의 `Total` 속성을 통해 전체 데이터 건수를 가져오면, 페이지 단위로 나누어 조회됩니다.  
> 최초 1회 호출하면 이후 페이지 이동, Sort 등은 시트가 자동으로 서버에 요청합니다.  
> 비동기형식으로 동작하므로, 서버 응답의 Total 등을 가공하려면 [onReceiveData](/docs/events/on-receive-data), Data 배열을 가공하려면 [onBeforeDataLoad](/docs/events/on-before-data-load) 이벤트에서 처리하세요.  
> 서버 응답(JSON) 구조와 관련된 상세 내용은 [페이징 응답 규격](/docs/dataStructure/paging-structure)을 참고하세요.  
> 조회 시 자동 포커스 [(Cfg)IgnoreFocused](/docs/props/cfg/ignore-focused), 메시지 표시 [(Cfg)SuppressMessage](/docs/props/cfg/suppress-message)를 참고하세요.

### Syntax
```javascript
void doSearchPaging( url, pageParam, param, reqHeader, method, callback, timeout, sync, strictParse, traditional, restapi, cPage, pageLengthParam, beforeSend, orderByParam );
```

### Parameters

|Name|Type|Required|Description|
|----------|-----|---|----|
|url|`string`|<span class='required'>필수</span>|ajax를 통해 호출할 url|
|pageParam|`string`|<span class='optional'>선택</span>|서버로 전송할 페이지 변수 (`default: 'ibpage'`)|
|param|`string` \| `object`|<span class='optional'>선택</span>|서버로 전송할 조회 조건 파라미터|
|reqHeader|`object`|<span class='optional'>선택</span>|서버 전송시 request header에 정의할 내용<br/>ex : `{"callBy":"ibsheetObject","method":"doSearchPaging"}`|
|method|`string`|<span class='optional'>선택</span>|GET/POST 선택 (`default: 'GET'`)|
|callback|`function`|<span class='optional'>선택</span>|조회 후 호출할 콜백 함수|
|timeout|`number`|<span class='optional'>선택</span>|서버 통신 최대 대기 시간 (단위: 초(second), `default: 60`)|
|sync|`number`|<span class='optional'>선택</span>|동기 조회 여부. 비동기일 경우 연속으로 호출시 이전 조회가 종료되지 않으면 이후의 조회는 무시됩니다. 연속으로 호출해야 되고, 반드시 모든 조회가 완료되어야 한다면 동기 조회 모드를 사용해야 합니다.<br/>`0`:비동기 방식 (`default`)<br/>`1`:비동기 순차 처리 방식<br/>`2`:동기 방식|
|strictParse|`boolean`|<span class='optional'>선택</span>|JSON 파서 선택<br>`0(false)`:유연한 파서 사용 (`default`) — 여분의 콤마, 프로퍼티 이름 쌍따옴표 생략 허용<br>`1(true)`:브라우저 JSON.parse() 사용 (약 5배 빠르나 5만건 이내에서는 차이 미미)|
|traditional|`boolean`|<span class='optional'>선택</span>|서버로 배열 param 전송 시 형식 설정<br/>`param: {"data": [1, 2]}` 일 때<br/>`0(false)`: `data[]=1&data[]=2` (`default`)<br/>`1(true)`: `data=1&data=2`|
|restapi|`boolean`|<span class='optional'>선택</span>|페이지 URL 주소 형식이 REST API 주소형식에 맞게 변경되도록 하는 설정<br/>`0(false)`:페이지 URL 주소 변경 기능 사용 안함 (`default`)<br/>`1(true)`:페이지 URL 주소 REST API 주소형식에 맞게 변경 기능 사용<br><br> **<mark>주의</mark> : GET 방식으로 보낼 경우 pageParam을 제외한 다른 파라미터들은 전송되지 않음** <br/>ex) `/userInfo/users/2`|
|cPage| `number`|<span class='optional'>선택</span>|조회 시 처음 보여질 페이지 번호 (1부터 시작)|
|pageLengthParam| `string`|<span class='optional'>선택</span>|서버로 전송할 `pageLength` 변수 (`default: 'ibpagelength'`)|
|beforeSend|`function`|<span class='optional'>선택</span>|조회 전 호출할 함수<br/>`1(true)` 값을 리턴 시 조회가 취소|
|orderByParam|`string`|<span class='optional'>선택</span>|서버로 전송할 소팅 정보 파라미터 이름을 변경하고 싶은 경우 설정합니다. (`default: 'iborderby'`)|


### Return Value
***none***

### Example
```javascript
// SearchMode 3, 4, 5 에서 사용
options.Cfg = {
    SearchMode: 4,
    PageLength: 100
};
```

```javascript
// Form Data 방식 (쿼리스트링)
var opt = {
  "url":"/cust/getCustInfo.do",
  "param":"custId=92123&empId=24342",
  "method":"POST",
  "beforeSend":function (rtn) {
    console.log(rtn.sheet);  // 시트 객체
   },
  "callback":function (rtn) {
    var rtnData = JSON.parse(rtn.data);
    alert("전체 데이터 건수 :" + rtnData["Total"]);
  }
};
sheet.doSearchPaging(opt);

// Form Data 방식 (object)
sheet.doSearchPaging({
    url: "/cust/getCustInfo.do",
    param: { custId: "92123", empId: "24342" },
    method: "POST"
});
// → Form Data: custId=92123&empId=24342&ibpage=1&ibpagelength=50

// JSON Payload 방식 (object + reqHeader)
sheet.doSearchPaging({
    url: "/cust/getCustInfo.do",
    param: { custId: "92123", empId: "24342" },
    reqHeader: { "Content-Type": "application/json" },
    method: "POST"
});
// → Request Payload: {"custId":"92123","empId":"24342","ibpage":1,"ibpagelength":50}

// 인증 토큰 전송
sheet.doSearchPaging({
    url: "/cust/getCustInfo.do",
    param: { custId: "92123" },
    method: "POST",
    reqHeader: { "Authorization": "Bearer eyJhbGciOiJIUzI1..." }
});

//조회 데이터 예시
{
  "Total":254141,   //전체 데이터 건수
  "Data":[
    {},...,{}   //PageLength에서 설정한 건수만큼 조회
  ]
}
```

### Read More

- [SearchMode cfg](/docs/props/cfg/search-mode)
- [조회 이벤트 발생 순서](/docs/events/02-search-event-flow)
- [PageLength cfg](/docs/props/cfg/page-length)
- [SortCurrentPage cfg](/docs/props/cfg/sort-current-page)
- [ScrollPagingServerSort cfg](/docs/props/cfg/scroll-paging-server-sort)
- [InfoRowConfig cfg](/docs/props/cfg/info-row-config)
- [Timeout cfg](/docs/props/cfg/timeout)
- [페이징 응답 규격](/docs/dataStructure/paging-structure)
- [onReceiveData event](/docs/events/on-receive-data)
- [onDataLoad event](/docs/events/on-data-load)
- [SuppressMessage cfg](/docs/props/cfg/suppress-message)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.0.0.5|`timeout` 인자 추가|
|core|8.0.0.6|`sync` 인자 추가|
|core|8.0.0.7|`strictParse`, `traditional`, `restapi` 인자 추가|
|core|8.0.0.20|`cPage` 인자 추가|
|core|8.1.0.41|`pageLengthParam` 인자 추가|
|core|8.1.0.49|`beforeSend` 인자 추가|