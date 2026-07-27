# getPageIndex ***(method)***
> 페이지의 `index`를 확인합니다.
>
> `index`는 `0`부터 시작합니다.


### Syntax
```javascript
number getPageIndex( page );
```

### Parameters
|Name|Type|Required| Description |
|----------|-----|---|----|
|page|`object`|<span class='required'>필수</span>|페이지 데이터 객체


### Return Value
***number*** : [페이지 객체](/docs/appx/page-object)의 index 번호

### Example
```javascript
//현재 포커스가 위치한 페이지
var page = sheet.getFocusedPage();
//페이지 인덱스 확인
var pidx = sheet.getPageIndex(page);
```

### Read More
- [getPageByIndex method](./get-page-by-index)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
