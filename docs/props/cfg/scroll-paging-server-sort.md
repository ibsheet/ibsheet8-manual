# ScrollPagingServerSort ***(cfg)***

<!-- synonyms: ScrollPagingServerSort, scroll paging server sort, server side sort, SearchMode 3 sort, scroll paging sort, 서버 정렬, 서버 소팅, 스크롤 페이징 서버 소팅, 서버 사이드 소팅, SearchMode 3 정렬 -->

> 스크롤 페이징 사용 시([SearchMode](./search-mode): 3)을 사용하며 서버 소팅을 사용하고 싶은 경우 설정하는 옵션입니다. 설정시, 소팅할 때 소팅 정보를 서버에 보내고, 결과를 조회합니다.

### Type
`boolean`

### Options
|Value|Description|
|---|---|
|`0(false)`|Sort 정보를 서버에 보내지 않고, 현재 보여지는 페이지에 대해서만 정렬합니다. (`default`)|
|`1(true)`|Sort 정보를 서버에 보내고, 결과를 조회합니다.|

### 참고

> 서버로 `iborderby=컬럼명^ASC` 형식의 파라미터가 전송됩니다. 다중 정렬 시 `|`로 구분됩니다.  
> (예: `iborderby=col1|col2^ASC|ASC`)  
> 파라미터 이름을 변경하려면 [doSearchPaging](/docs/funcs/core/do-search-paging)의 `orderByParam`을 참고하세요.
>
> **<mark>보안 주의</mark>** : 서버에서 이 값을 SQL에 직접 삽입하지 마세요. (SQL Injection)

### Example
```javascript
options.Cfg = {
    SearchMode: 3,
    PageLength: 100,
    ScrollPagingServerSort: true  // Sort 정보를 서버로 전송
};
```

### Read More

- [SearchMode cfg](./search-mode)
- [SortCurrentPage cfg](./sort-current-page)
- [doSearchPaging method](/docs/funcs/core/do-search-paging)

### Since

|product|version|desc|
|---|---|---|
|core|8.2.0.6|기능 추가|
