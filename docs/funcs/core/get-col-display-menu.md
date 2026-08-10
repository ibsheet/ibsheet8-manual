# getColDisplayMenu ***(method)***

<!-- synonyms: getColDisplayMenu, get-col-display-menu, 열 표시 메뉴, 컬럼 메뉴, 열 표시 설정, 메뉴 객체, 열 숨김 메뉴, 표시 메뉴, column, menu, display -->

> 현재 시트에 표시되는 열들의 표시 여부를 설정할 수 있는 메뉴 객체를 리턴합니다.
>
> 이 메뉴는 [showMenu](/docs/static/show-menu)를 사용하여 특정 위치에 표시할 수 있습니다.

![getColDisplayMenu](/assets/imgs/colDisplayMenu.png "ColDisplayMenu")<br/>
[메뉴 이미지]<br/>

### Syntax
```javascript
object getColDisplayMenu();
```

### Return Value
***object*** : 메뉴 객체

### Example
```javascript
// 마우스 위치에 '컬럼 표시 여부' 메뉴 표시 예시
var menu = sheet.getColDisplayMenu();

IBSheet.showMenu(menu, {Mouse: 1});
```

### Read More
- [Menu appendix](/docs/appx/menu)
- [showMenu static](/docs/static/show-menu)
- [showMenu method](./show-menu)

### Since

|product|version|desc|
|---|---|---|
|core|8.3.0.51|기능 추가|
