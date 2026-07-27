# goToPage ***(method)***
> 특정 페이지로 이동합니다.


### Syntax
```javascript
void goToPage( page );
```

### Parameters
|Name|Type|Required| Description |
|----------|-----|---|----|
|page|`object`|<span class='required'>필수</span>|[데이터 페이지 객체](/docs/appx/page-object)|


### Return Value
***none***

### Example
```javascript
//마지막 페이지를 얻음
var page = sheet.getPageByRow(sheet.getLastRow() );
//마지막 페이지로 이동
sheet.goToPage(page);
```

### Read More
- [goToNextPage method](./go-to-next-page)
- [goToPrevPage method](./go-to-prev-page)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
