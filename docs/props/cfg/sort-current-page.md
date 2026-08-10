# SortCurrentPage ***(cfg)***

<!-- synonyms: SortCurrentPage, sort current page, current page sort only, server paging sort, SearchMode 4 5 sort, page only sort, 현재 페이지 정렬, 현재 페이지만 소팅, 서버 페이징 소팅, SearchMode 4 5 정렬, 로컬 페이지 정렬 -->

> 서버 페이징 사용 시([SearchMode](./search-mode): 4, 5) 현재 보여지는 페이지에 대해서만 정렬할지 여부를 설정합니다.

### Type
`boolean`

### Options
|Value|Description|
|---|---|
|`0(false)`|Sort 정보를 서버에 보내고, 결과를 조회합니다. (`default`)|
|`1(true)`|Sort 정보를 서버에 보내지 않고, 현재 보여지는 페이지에 대해서만 정렬합니다.|

### 참고

> 서버로 `iborderby=컬럼명^ASC` 형식의 파라미터가 전송됩니다. 다중 정렬 시 `|`로 구분됩니다.  
> (예: `iborderby=col1|col2^ASC|ASC`)  
> 파라미터 이름을 변경하려면 [doSearchPaging](/docs/funcs/core/do-search-paging)의 `orderByParam`을 참고하세요.
>
> **<mark>보안 주의</mark>** : 서버에서 이 값을 SQL에 직접 삽입하지 마세요. (SQL Injection)

### Example
```javascript
options.Cfg = {
    SearchMode: 4,
    PageLength: 100,
    SortCurrentPage: true  // 현재 페이지에 대해서만 정렬
};
```

### Read More

- [SearchMode cfg](./search-mode)
- [ScrollPagingServerSort cfg](./scroll-paging-server-sort)
- [doSearchPaging method](/docs/funcs/core/do-search-paging)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
