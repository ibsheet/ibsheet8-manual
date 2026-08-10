# getBodyHeight ***(method)***

<!-- synonyms: getBodyHeight, get-body-height, 바디 높이, 데이터 영역 높이, 시트 높이, 높이 조회, 높이 확인, 픽셀 높이, height, body -->

> 시트 데이터 영역의 높이를 리턴합니다.
>
> 헤더나 필터 행의 높이는 포함되지 않습니다.


### Syntax
```javascript
number getBodyHeight( );
```


### Return Value
***number*** : 데이터 영역의 높이 (pixel 단위)

### Example
```javascript
//데이터 영역의 높이를 리턴함. (세로 스크롤과 무관함)
var h = sheet.getBodyHeight( );
```

### Read More
- [getRowTop method](./get-row-top)
- [getScrollTop method](./get-scroll-top)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
