# PageLength ***(cfg)***

<!-- synonyms: PageLength, page length, page size, rows per page, paging size, 페이지 크기, 페이지 행 수, 페이지 당 행 개수, 페이징 사이즈, 한 페이지 행 수, SearchMode 페이징, 서버 페이징 크기, 페이징 개수 -->

> 한 페이지(`Page`)에 표시할 행(`Row`)의 개수를 설정합니다.  
> `SearchMode: 2 (LazyLoad)`는 전체 데이터를 조회하되, 한 번에 화면에 표시(렌더링)되는 데이터가 `PageLength`와 `MaxPages`(default 1)로 계산된 개수만큼입니다.  
> `SearchMode: 1,2,4,5`로 조회 시 PageLength의 값이 너무 크면 성능이 떨어집니다. 20~100개 설정 권장합니다.  
> **주의 : 서버페이징(SearchMode: 3,4,5) 사용 시 PageLength 값과 서버에서 받아오는 데이터의 개수를 반드시 맞춰주셔야 합니다.(PageLength 설정하지 않았을 경우 기본값은 20입니다)**


### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`number`|한 페이지 단위의 행 수 (`default: 20`)|


### Example
```javascript
options = {
    Cfg :{
      PageLength: 30,  // 한 페이지당 표시할 행 수
      MaxPages: 5      // 렌더링될 페이지 수를 설정
    }
};
```

### Read More
- [SearchMode cfg](/docs/props/cfg/search-mode)
- [MaxPages cfg](/docs/props/cfg/max-pages)
- [goToPage method](/docs/funcs/core/go-to-page)
- [updateClientPaging method](/docs/funcs/core/update-client-paging)
- [updatePageLength method](/docs/funcs/core/update-page-length)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
