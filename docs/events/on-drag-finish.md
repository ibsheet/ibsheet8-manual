# onDragFinish ***(event)***

<!-- synonyms: 드래그 완료, 드래그 종료, 드롭 후 최종, on-drag-finish, drag finish, drag complete, drop end -->

> 드래그된 행들이 드랍된 후, 가장 마지막에 발생하는 이벤트입니다.  
> 이 이벤트는 대상 시트(`tosheet`)에 드래그 결과가 모두 반영된 이후 호출됩니다.  
> 시트 간 이동 시 이 이벤트는 **드래그 시작 시트에서만 발생**합니다.

### Syntax

```
    onDragFinish : function(paramObject) {

    }
or
    sheet.bind("onDragFinish" , function(paramObject) {});
```

### Parameters
| Name | Type | Description |
|----------|-----|-------|
|sheet|`object`|드래그가 시작된 시트 객체|
|row|`object`|이동할 행의 [데이터 로우 객체](/docs/appx/row-object)|
|tosheet|`object`|행이 이동할 대상 시트 객체|
|torow|`object`|드랍될 위치 기준의 [데이터 로우 객체](/docs/appx/row-object)|

### Return
***none***


### Example
```javascript
options.Events = {
    onDragFinish:function(evtParam){
        // 해당 구간은 드래그가 끝난 뒤 시트에 반영된 상태입니다.
    }
}
```

### Read More
- [드래그 앤 드롭 이벤트 발생 순서](/docs/events/10-drag-event-flow)
- [CanDrag cfg](/docs/props/cfg/can-drag)
- [DragCopy cfg](/docs/props/cfg/drag-copy)
- [onStartDrag event](./on-start-drag)
- [onEndDrag event](./on-end-drag)
- [onAfterRowMoveTosheet event](./on-after-row-move-to-sheet)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.15|기능 추가|
