# onRenderFirstFinish ***(event)***

<!-- synonyms: 최초 렌더링 완료, 시트 최초 생성 후, 첫 렌더 완료, on-render-first-finish, first render finish, initial render -->

> 시트가 **처음** 생성되어 렌더링될 때 호출되는 이벤트 입니다. **(최초 1회만 발생)**
>
> 데이터 없이 시트 생성 함수(IBSheet.create)를 호출한 경우 onRenderFirstFinish 이벤트에서 시트에 데이터를 넣을 수 있습니다.

### Syntax

```
    onRenderFirstFinish : function(paramObject) {

    }
or
    sheet.bind("onRenderFirstFinish" , function(paramObject) {});
```

### Parameters


| Name | Type | Description |
|----------|-----|-------|
|sheet|`object`|처음 생성된 시트 객체|

### Return
***none***


### Example
```javascript
var data = [
    {"chgrDptNm":"전략기획","taskId":"100201","actnEndTm":"190000","ordr":"1","preTaskId":"100200"},
    {"chgrDptNm":"실행예산","taskId":"100204","actnEndTm":"170000","ordr":"2","preTaskId":"100200"}
];

options.Events = {
    onRenderFirstFinish: function(evtParam){
        // 시트에 데이터를 넣습니다.
        evtParam.sheet.loadSearchData(data);
    }
}
```

### Read More

- [rerender method](/docs/funcs/core/rerender)
- [loadSearchData method](/docs/funcs/core/load-search-data)
- [doSearch method](/docs/funcs/core/do-search)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
