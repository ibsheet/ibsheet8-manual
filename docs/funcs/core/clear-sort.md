# clearSort ***(method)***

<!-- synonyms: 정렬 취소, 소팅 취소, 정렬 초기화, 정렬 해제, clear sort, 정렬 아이콘 제거 -->

> 헤더에 적용된 정렬을 취소합니다.  
> 헤더의 정렬 아이콘이 사라지고, 데이터는 조회(로드)된 원래 순서로 돌아갑니다.  
> 조회해도 정렬 상태는 유지되므로([doSearch](./do-search) 참고), 재조회 시 이전 정렬 기준으로 다시 정렬되는 것을 막으려면 조회 전에 이 함수를 호출합니다.

### Syntax
```javascript
void clearSort( );
```

### Return Value
***none***

### Example
```javascript
//헤더 소팅된 내용을 원래 순서로 클리어
sheet.clearSort();
```

### Read More
- [doSort method](./do-sort)
- [doSearch method](./do-search)
- [loadSearchData method](./load-search-data)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
