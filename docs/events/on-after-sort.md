# onAfterSort ***(event)***

<!-- synonyms: 정렬 후, 소팅 완료, 정렬 이후 처리, on-after-sort, after sort, sorted, sorting done -->

> 소팅이 이루어진 후 호출되는 이벤트입니다.

### Syntax

```
    onAfterSort:function(paramObject) {

    }
or
    sheet.bind("onAfterSort" , function(paramObject) {});
```

### Parameters
| Name | Type | Description |
|----------|-----|------------|
|sheet|`object`|소팅이 실행된 시트 객체|

### Return
***none***



### Example
```javascript
options.Events = {
    onAfterSort:function(evtParam){
        // 모든 정렬이 다 끝난 후 호출되기에 여기서 상태 메시지를 띄운다.
        alert("정렬이 완료되었습니다.");
    }
}
```

### Read More

- [컬럼 소팅(정렬) 이벤트 발생 순서](/docs/events/08-sort-event-flow)
- [onBeforeSort event](./on-before-sort)
- [doSort method](/docs/funcs/core/do-sort)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
