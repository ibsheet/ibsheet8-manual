# setScrollLeft ***(method)***

<!-- synonyms: setScrollLeft, set-scroll-left, 가로 스크롤, 좌우 스크롤, 스크롤 이동, 수평 스크롤, x축 이동, 스크롤 위치, 좌측 이동, scroll left, horizontal scroll, set scroll, scroll x, move scroll -->

> 가로스크롤 바를 pixel단위로 이동시킵니다.

### Syntax
```javascript
boolean setScrollLeft( pos, section );
```

### Parameters
|Name|Type|Required| Description |
|----------|-----|---|----|
|pos|`number`|<span class='required'>필수</span>|x축 기준 이동할 거리|
|section|`number`|<span class='optional'>선택</span>|틀고정을 기준으로 한 좌우 영역<br>`0`:좌측<br>`1`:가운데(`default`)<br>`2`:우측|

### Return Value
***boolean*** : 이동여부 (동일한 위치로 pos 설정시 `0(false)` 리턴)

### Example
```javascript
//현재 가로스크롤 바의 위치를 얻는다.
var offset = sheet.getScrollLeft(1);
//다시 렌더링
sheet.rerender();
//원래 위치로 이동시킴
sheet.setScrollLeft(offset, 1);
```

### Read More
- [getScrollLeft method](./get-scroll-left)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
