# getPageByIndex ***(method)***
> 특정 `index`를 갖는 [페이지 객체](/docs/appx/page-object)를 리턴합니다.
>
> `index`는 `0`부터 시작합니다.


### Syntax
```javascript
object getPageByIndex( index );
```

### Parameters
|Name|Type|Required| Description |
|----------|-----|---|----|
|index|`number`|<span class='required'>필수</span>|얻고자하는 페이지 순서 번호


### Return Value
***page object*** : 지정한 순서에 해당하는 [페이지 객체](/docs/appx/page-object)

### Example
```javascript
//15번 페이지 객체를 얻음
var pageObj = sheet.getPageByIndex(15);
```

### Read More
- [getPageIndex method](./get-page-index)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
