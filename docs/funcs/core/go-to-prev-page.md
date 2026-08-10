# goToPrevPage ***(method)***

<!-- synonyms: goToPrevPage, go-to-prev-page, 이전 페이지, 페이지 이동, 이전 이동, 페이지 넘김, 뒤로 이동, 이동, 넘기기, go, previous, prev, page, move, back -->

> 현재 페이지의 이전 페이지로 이동합니다.


### Syntax
```javascript
boolean goToPrevPage();
```

### Return Value
***boolean*** : 페이지 이동 성공여부(현재 페이지가 첫페이지인 경우 false가 리턴)

### Example
```javascript
//이전페이지로 이동
function PrevPage(){
    var rtn = sheet.goToPrevPage();
    if (!rtn) {
        alert("첫 페이지 입니다.");
    }
}
```

### Read More
- [goToPage method](./go-to-page)
- [goToNextPage method](./go-to-next-page)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
