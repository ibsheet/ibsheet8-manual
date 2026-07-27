# onRenderFirstFinishAll ***(static)***

> `IBSheet` 객체에 선언된 시트가 모두 생성된 이후 발생하는 일종의 이벤트 입니다.<br/>
> 해당 함수에 시트가 모두 생성된 후 처리할 작업을 작성합니다. <br/>

### Syntax
```javascript
IBSheet.onRenderFirstFinishAll = function(obj){
    ...
};
```

### Parameters
| Name | Type | Description |
|----------|----|----|
|sheet|`object`|마지막에 생성된 시트 객체|

### Return Value
***None***

### Example
```javascript
var data = [
    {"chgrDptNm": "전략기획", "taskId": "100201", "actnEndTm": "190000", "ordr": "1", "preTaskId": "100200"},
    {"chgrDptNm": "실행예산", "taskId": "100204", "actnEndTm": "170000", "ordr":"2", "preTaskId": "100200"}
];

IBSheet.onRenderFirstFinishAll = function(obj){
    //시트가 모두 생성 된 후 처리할 작업
    obj.sheet.loadSearchData(data);
};
```

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.5|기능 추가|