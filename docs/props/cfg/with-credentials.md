# WithCredentials ***(cfg)***

<!-- synonyms: WithCredentials, with credentials, ajax credentials, xhr withCredentials, CORS credentials, cookie ajax, ajax 쿠키, CORS 인증, 인증 정보 포함 요청, 크로스 도메인 쿠키, 크로스 오리진 인증 -->

> [doSearch](/docs/funcs/core/do-search), [doSearchPaging](/docs/funcs/core/do-search-paging), [doSave](/docs/funcs/core/do-save) 사용시 내부 Ajax 요청에서 [withCredentials](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/withCredentials) 옵션을 설정할 수 있습니다.
>
> 쿠키나 인증 정보를 포함해야 하는 요청에 유용합니다.
>
> **주의:** `WithCredentials: true`를 사용할 경우, 서버에서 CORS 설정이 필요합니다.  
> 1. `Access-Control-Allow-Origin`을 `"*"` 대신 요청하는 도메인(origin)으로 설정  
> 2. `Access-Control-Allow-Credentials: true` 설정  
> 3. 필요한 경우 `Access-Control-Allow-Methods` 및 `Access-Control-Allow-Headers` 설정  
> 서버 설정이 올바르지 않으면 브라우저에서 요청이 차단됩니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|Ajax 요청 시 withCredentials 사용 안함 (`default`)|
|`1(true)`|Ajax 요청 시 withCredentials 옵션 사용|

### Example
```javascript
options.Cfg = {
    WithCredentials: true // Ajax 요청에 쿠키/인증 정보 포함
};
```

### Read More
- [doSearch method](/docs/funcs/core/do-search)
- [doSearchPaging method](/docs/funcs/core/do-search-paging)
- [doSave method](/docs/funcs/core/do-save)

### Since

|product|version|desc|
|---|---|---|
|core|8.1.0.28|기능 추가|
