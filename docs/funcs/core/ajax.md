# ajax ***(method)***

<!-- synonyms: 서버 통신, 데이터 요청, ajax 통신, http 요청, 비동기 요청, 서버 호출, 데이터 가져오기, ajax, xhr, request, http, fetch, async -->

> ajax 통신을 통해 서버로부터 데이터를 받아옵니다.
>
> 서버 통신이 완료되었을때 실행되는 callback 함수를 이용해서 서버로부터 받은 데이터를 사용할 수 있습니다.

### Syntax
```javascript
void ajax ( url, param, method, callback, sync, reqHeader, timeout, traditional );
```

### Parameters

|Name|Type|Required|Description|
|----------|-----|---|----|
|url|`string`|<span class='required'>필수</span>|ajax를 통해 호출할 url|
|param|`string` \| `object`|<span class='optional'>선택</span>|서버로 전송할 파라미터|
|method|`string`|<span class='optional'>선택</span>| 전송방식 `GET / POST` 선택 (`default: 'GET'`)|
|callback|`function`|<span class='optional'>선택</span>|서버 통신이 완료되었을때 발생하는 콜백 함수<br/>ex) `func(res(결과 코드), data(서버로부터 받은 데이터, string), responseXML(XMLHttpRequest.responseXML), response(XMLHttpRequest 객체))`|
|sync|`boolean`|<span class='optional'>선택</span>|동기식 처리 여부<br/>`0(false)`:비동기 방식 (`default`)<br/>`1(true)`:동기 방식|
|reqHeader|`object`|<span class='optional'>선택</span>|서버로 전송할 헤더 {key1: value1, key2: value2}|
|timeout|`number`|<span class='optional'>선택</span>|서버 통신 최대 대기 시간 (단위: 초(second), `default: 60`)|
|traditional|`boolean`|<span class='optional'>선택</span>|서버로 배열 param 전송 시 형식 설정<br/>`param: {"data": [1, 2]}` 일 때<br/>`0(false)`: `data[]=1&data[]=2` (`default`)<br/>`1(true)`: `data=1&data=2`|

### Return Value
***none***

### Example
```javascript
// POST 방식으로 데이터 조회
sheet.ajax("./insaAppMain.do", "dept_cd=031&position_cd=A0", "POST", function (res, data, resXml, response) {
  if (res >= 0) {
    sheet.loadSearchData(data);
  } else {
    alert("데이터 조회에 실패 했습니다!!");
  }
});

// GET 방식으로 데이터 조회
sheet.ajax({
  url: "./insaAppMain.do",
  param: {"dept_cd": 31, "position_cd": "A0"},
  method: "GET",
  reqHeader: {"Content-Type":"application/json"},
  callback: function (res, data, resXml, response) {
    if (res >= 0) {
      sheet.loadSearchData(data);
    } else {
      alert("데이터 조회에 실패 했습니다");
    }
  }
});
```

### Read More
- [loadSearchData method](./load-search-data)
- [Timeout cfg](/docs/props/cfg/timeout)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.0.0.5|`timeout` 인자 추가|
|core|8.0.0.7|`traditional` 인자 추가|
|core|8.0.0.17|`params` -> `param` 인자명 변경 (`params` 사용 가능)|