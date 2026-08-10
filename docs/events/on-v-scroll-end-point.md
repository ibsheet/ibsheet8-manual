# onVScrollEndPoint ***(event)***

<!-- synonyms: 세로 스크롤 끝점, 스크롤 끝, 스크롤 최상단, 스크롤 최하단, 무한 스크롤, 스크롤 끝 도달, on-v-scroll-end-point, vertical scroll end, scroll end point, scroll edge -->

> 시트의 세로 스크롤이 가장 처음과 가장 마지막일때 발생하는 이벤트입니다.
>
> `vpos` 인자가 0이면 가장 상단을 의미하고 `vpos`가 0이 아닐때는 가장 하단을 의미합니다.

### Syntax

```
    onVScrollEndPoint : function(paramObject) {

    }
or
    sheet.bind("onVScrollEndPoint" , function(paramObject) {});
```

### Parameters
| Name | Type | Description |
|----------|-----|-------|
|sheet|`object`|스크롤을 움직인 시트 객체|
|vpos|`number`|움직인 후 중간 섹션(section)의 scrollTop(pixel 단위)|
|oldvpos|`number`|움직이기전 중간 섹션(section)의 scrollTop(pixel 단위)|

### Return
***none***


### Example
```javascript
options.Events = {
    onVScrollEndPoint:function(evtParam){
        if (evtParam.vpos) {
            console.log('세로 스크롤 끝!!!');
            var params = {
                "url": "./DoSearch.do",
                "param": "param1=10&param2=ABC",
                "method": "POST",
                "append": true,
                "callback": function (rtn) {
                    var rtnData = JSON.parse(rtn.data);
                    console.log(rtnData);
                }
            };
            evtParam.sheet.doSearch(params);
        }
    }
}
```

### Read More
- [onScroll event](./on-scroll)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.5|기능 추가|
