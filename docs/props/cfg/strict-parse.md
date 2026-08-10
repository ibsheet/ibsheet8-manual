# StrictParse ***(cfg)***

<!-- synonyms: StrictParse, strict parse, json parse strict, native json parse, flexible json parse, JSON.parse, 엄격 파싱, JSON 엄격 파싱, JSON.parse 사용, 유연한 파서, JSON 파서 선택, doSearch 파싱 -->

> 조회 함수에서 JSON 데이터를 파싱할 때 파서를 선택합니다.
>
> 설정을 안하거나 false로 설정시 유연한 파서를 통해 파싱되고, true로 설정시 브라우져가 제공하는 JSON.parse()를 통해 파싱됩니다.
>
> **[doSearch](/docs/funcs/core/do-search), [doSearchPaging](/docs/funcs/core/do-search-paging), [loadSearchData](/docs/funcs/core/load-search-data) 호출 시 strictParse 인자가 설정되지 않았을 경우에 적용되며 API의 strictParse 인자가 우선 적용됩니다.**

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|유연한 파서 사용 (`default`) — 여분의 콤마, 프로퍼티 이름 쌍따옴표 생략 허용|
|`1(true)`|브라우저 JSON.parse() 사용 (약 5배 빠르나 5만건 이내에서는 차이 미미)|

### Example
```javascript
options.Cfg = {
    StrictParse: 1,       // 조회 함수를 JSON.parse()를 통해 데이터 파싱  
};
```

### Read More
- [doSearch method](/docs/funcs/core/do-search)
- [doSearchPaging method](/docs/funcs/core/do-search-paging)
- [loadSearchData method](/docs/funcs/core/load-search-data)

### Since
|product|version|desc|
|---|---|---|
|core|8.0.0.7|기능 추가|
