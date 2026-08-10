# onAfterColMove ***(event)***

<!-- synonyms: 열 이동 후, 컬럼 이동 완료, 컬럼 순서 변경 후, moveCol 이후, on-after-col-move, after column move, column moved -->

> 열을 드래그를 통해 다른 위치로 움직인 후 호출되는 이벤트입니다.

### Syntax

```
    onAfterColMove : function(paramObject) {

    }
or
    sheet.bind("onAfterColMove" , function(paramObject) {});
```

### Parameters
| Name | Type | Description |
|----------|-----|-------|
|sheet|`object`|시트 객체|
|col|`string`|드래그된 열의 열이름|

### Return
***none***

### Example
```javascript
options.Events = {
    onAfterColMove:function(evtParam){
        // 변경된 열이름과 그 변화량을 alert로 보여줍니다.
        alert(evtParam.col+"열의 드래깅이 완료되었습니다.");
    }
}
```

### Read More
- [onBeforeColMove event](./on-before-col-move)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
