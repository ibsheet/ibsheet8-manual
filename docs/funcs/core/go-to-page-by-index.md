# goToPageByIndex ***(method)***

<!-- synonyms: goToPageByIndex, go-to-page-by-index, 페이지 인덱스, 페이지 번호, 페이지 이동, 인덱스 이동, 지정 이동, 이동, 넘기기, go, page, index, move, navigate -->

> 특정 페이지로 이동합니다.
>
> 클라이언트/서버 페이징에서 사용 가능합니다.


### Syntax
```javascript
void goToPageByIndex(index);
```

### Parameters
|Name|Type|Required| Description |
|----------|-----|---|----|
|index|`number`|<span class='required'>필수</span>|조회할 페이지 순서 번호


### Return Value
***none***

### Example
```javascript
//12번째 페이지로 이동
sheet.goToPageByIndex(12);
```

### Read More
- [goToNextPage method](./go-to-next-page)
- [goToPrevPage method](./go-to-prev-page)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
