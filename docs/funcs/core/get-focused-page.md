# getFocusedPage ***(method)***

<!-- synonyms: getFocusedPage, get-focused-page, 포커스 페이지, 현재 페이지, 활성 페이지, 페이지 객체, 포커스된 페이지, 페이지 조회, focused, page, current -->

> 현재 포커스가 위치한 데이터 [페이지 객체](/docs/appx/page-object)를 리턴합니다.

### Syntax
```javascript
object getFocusedPage();
```

### Return Value
***page object*** : [페이지 객체](/docs/appx/page-object)

### Example
```javascript
//현재 포커스가 있는 페이지 객체
var pageObj = sheet.getFocusedPage();
```

### Read More
- [getPageIndex method](./get-page-index)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
