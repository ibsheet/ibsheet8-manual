# onAfterExpand ***(event)***
> 트리 사용시 트리가 접히거나 펼쳐진 후 호출됩니다.

### Syntax

```
    onAfterExpand : function(paramObject) {

    }
or
    sheet.bind("onAfterExpand" , function(paramObject) {});
```

### Parameters
| Name | Type | Description |
|----------|-----|-------|
|sheet|`object`|시트 객체|
|row|`object`|펼쳐진/접힌 행 [데이터 로우 객체](/docs/appx/row-object)|


### Return
***none***

### Example
```javascript
options.Events = {
    onAfterExpand:function(evtParam){
        // 펼쳐진 행의 레벨이 4 이상인 경우 카운트
        if(evtParam.row["Level"] >= 4){
            LevCount++;
        }
    }
}
```

### Read More

- [트리 확장/접기 이벤트 발생 순서](/docs/events/09-tree-event-flow)
- [setExpandRow method](/docs/funcs/core/set-expand-row)
- [showTreeLevel method](/docs/funcs/core/show-tree-level)
- [onBeforeExpand event](/docs/events/on-before-expand)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.4|기능 추가|
