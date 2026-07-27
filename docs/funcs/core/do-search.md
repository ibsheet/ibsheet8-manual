# doSearch ***(method)***

<!-- synonyms: 조회, 데이터 조회, 대기이미지, 로딩, 검색, search, data load, loading, ajax -->

> `doSearch`는 AJAX 통신을 통해 JSON 형식의 데이터를 시트에 로드합니다.  
> [SearchMode](/docs/props/cfg/search-mode) 0, 1, 2에서 사용합니다. (SearchMode 3, 4, 5는 [doSearchPaging](/docs/funcs/core/do-search-paging)을 사용)  
> AJAX 통신 없이 데이터만 바인딩하려면 [loadSearchData](/docs/funcs/core/load-search-data)를 사용하세요.  
> 비동기형식으로 동작하므로, 데이터 로드 후 처리는 [onReceiveData](/docs/events/on-receive-data), [onBeforeDataLoad](/docs/events/on-before-data-load), [onDataLoad](/docs/events/on-data-load) 이벤트에서 구현해야 합니다.  
> 기본적으로 `doSearch`는 시트의 기존 데이터를 제거하고 서버에서 가져온 데이터를 로드합니다.  
> 기존 데이터 뒤에 새 데이터를 추가하려면 `append: true` 옵션을 사용하세요.  
> 서버 응답(JSON) 구조와 관련된 상세 내용은 [조회 응답 규격](/docs/dataStructure/data-structure)을 참고하세요.  
> 조회 시 자동 포커스 [(Cfg)IgnoreFocused](/docs/props/cfg/ignore-focused), 메시지 표시 [(Cfg)SuppressMessage](/docs/props/cfg/suppress-message), 프로그레스바 [(Cfg)SearchProgress](/docs/props/cfg/search-progress)를 참고하세요.

### Syntax

```javascript
void doSearch( url, param, method, append, reqHeader, callback, timeout, sync, next, strictParse, traditional, parent );
```

### Parameters

|Name|Type|Required|Description|
|----------|-----|---|----|
|url|`string`|<span class='required'>필수</span>|AJAX를 통해 호출할 url|
|param|`string` \| `object`|<span class='optional'>선택</span>|서버로 전송할 파라미터|
|method|`string`|<span class='optional'>선택</span>| 전송방식 GET / POST 선택 (`default: 'GET'`)|
|append|`boolean`|<span class='optional'>선택</span>|기존 데이터에 `append` 여부<br/>조회 방식의 차이로 인해 `append:1(true)`사용 시 [SearchMode](/docs/props/cfg/search-mode):2인 경우 [onRenderFinish](/docs/events/on-render-finish)이벤트가 발생하지 않습니다.<br>`0(false)`:기존 데이터 제거 후 조회 데이터 로드 (`default`)<br>`1(true)`:기존 데이터에 조회 데이터 추가|
|reqHeader|`object`|<span class='optional'>선택</span>|서버 전송시 request header에 정의할 내용<br/>ex : `{"callBy":"ibsheetObject","method":"doSearch"}`|
|callback|`function`|<span class='optional'>선택</span>|조회 후 호출할 콜백 함수|
|timeout|`number`|<span class='optional'>선택</span>|서버 통신 최대 대기 시간 (단위: 초(second), `default: 60`)|
|sync|`number`|<span class='optional'>선택</span>|동기 조회 여부. 비동기일 경우 연속으로 호출시 이전 조회가 종료되지 않으면 이후의 조회는 무시됩니다. 연속으로 호출해야 되고, 반드시 모든 조회가 완료되어야 한다면 동기 조회 모드를 사용해야 합니다.<br/>`0`:비동기 방식 (`default`)<br/>`1`:비동기 순차 처리 방식<br/>`2`:동기 방식|
|next|`object`|<span class='optional'>선택</span>|[데이터 로우 객체](/docs/appx/row-object)<br/>지정한 행 위에부터 데이터 `append`. (`append:1(true)`일때만 사용 가능)|
|strictParse|`boolean`|<span class='optional'>선택</span>|JSON 파서 선택<br>`0(false)`:유연한 파서 사용 (`default`) — 여분의 콤마, 프로퍼티 이름 쌍따옴표 생략 허용<br>`1(true)`:브라우저 JSON.parse() 사용 (약 5배 빠르나 5만건 이내에서는 차이 미미)|
|traditional|`boolean`|<span class='optional'>선택</span>|서버로 배열 param 전송 시 형식 설정<br/>`param: {"data": [1, 2]}` 일 때<br/>`0(false)`: `data[]=1&data[]=2` (`default`)<br/>`1(true)`: `data=1&data=2`|
|parent|`object`|<span class='optional'>선택</span>|[데이터 로우 객체](/docs/appx/row-object)<br/> (동적 트리 조회 사용시 부모에 해당하는 행 지정) <br/>|


### Return Value
***none***

### Example

```javascript
// GET 방식으로 데이터 조회
sheet.doSearch("./insaAppMain.do", "dept_cd=031&position_cd=A0", "GET");

// POST - Form Data 방식 (reqHeader 미설정)
sheet.doSearch({
  url: "./insaAppMain.do",
  param: {"dept_cd": "031", "position_cd": "A0"},
  method: "POST"
});
// → Form Data: dept_cd=031&position_cd=A0

// POST - JSON Payload 방식 (Content-Type: application/json 설정)
sheet.doSearch({
  url: "./insaAppMain.do",
  param: {"dept_cd": "031", "position_cd": "A0"},
  method: "POST",
  reqHeader: {"Content-Type":"application/json"}
});
// → Request Payload: {"dept_cd":"031","position_cd":"A0"}

// 인증 토큰 전송
sheet.doSearch({
    url: "./insaAppMain.do",
    param: { dept_cd: "031" },
    method: "POST",
    reqHeader: { "Authorization": "Bearer eyJhbGciOiJIUzI1..." }
});
```

### Read More

- [SearchMode cfg](/docs/props/cfg/search-mode)
- [조회 이벤트 발생 순서](/docs/events/02-search-event-flow)
- [조회 응답 규격](/docs/dataStructure/data-structure)
- [loadSearchData method](./load-search-data)
- [doSearchPaging method](./do-search-paging)
- [onReceiveData event](/docs/events/on-receive-data)
- [onBeforeDataLoad event](/docs/events/on-before-data-load)
- [onDataLoad event](/docs/events/on-data-load)
- [onSearchFinish event](/docs/events/on-search-finish)
- [Timeout cfg](/docs/props/cfg/timeout)
- [SuppressMessage cfg](/docs/props/cfg/suppress-message)
- [SearchProgress cfg](/docs/props/cfg/search-progress)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.0.0.4|다른 API와 동일하게 제공하기 위해 `params` 인자명을 `param`으로 변경, 기존의 `params`를 사용할 수 있지만 권장하지 않음.|
|core|8.0.0.5|`timeout` 인자 추가|
|core|8.0.0.6|`sync` 인자 추가|
|core|8.0.0.7|`next`, `strictParse`, `traditional` 인자 추가|
|core|8.0.0.25|`parent` 인자 추가|
