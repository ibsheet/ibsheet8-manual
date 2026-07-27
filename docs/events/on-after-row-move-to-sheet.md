# onAfterRowMoveToSheet ***(event)***
> 서로 다른 시트 간에 행을 드래그 앤 드롭으로 이동할 때 호출되는 이벤트입니다.  
> 이 이벤트는 **드래그가 시작된 원본 시트에서만 발생**하며,  
> **같은 시트 내에서 행을 이동할 경우에는 호출되지 않습니다.**  
>
> 리턴 값에 따라 원본 시트에서 행을 삭제(삭제 상태로 변경), 제거(완전히 삭제), 유지(복사 처리)할지를 결정합니다.

<!-- synonyms: row move between sheets, drag row to sheet, move row to another sheet, cross sheet row move, 행 이동 이벤트, 시트 간 행 이동 -->

### Syntax
```
    onAfterRowMoveToSheet : function(paramObject) {

    }
or
    sheet.bind("onAfterRowMoveToSheet" , function(paramObject) {});
```

### Parameters
| Name | Type | Description |
|----------|-----|-------|
|sheet|`object`|드래그가 시작된 시트 객체|
|row|`object`|이동할 행의 [데이터 로우 객체](/docs/appx/row-object)|
|tosheet|`object`|행이 이동할 대상 시트 객체|
|torow|`object`|이동 후 대상 시트에 새로 생성된 [데이터 로우 객체](/docs/appx/row-object)|

<!--|copy|`boolean`|복사 여부 (`DragCopy` 설정값에 따라 결정됨)<br/>`0(false)`:이동<br/>`1(true)`:복사| -->

### Return
***number***

리턴 값에 따라 원본 시트의 행 처리 방식이 결정됩니다.

| Return Value |Description|
| -- | -- |
|`0(false)`|행을 이동한 것으로 간주, 기존 시트에서 행을 삭제 상태로 변경   |
|`1(true)` |행을 복사한 것으로 간주, 기존 시트에 행을 유지    |
|`-1`      |행을 이동한 것으로 간주, 기존 시트에서 행을 완전히 제거   |

### Example
```javascript
options.Events = {
    onAfterRowMoveToSheet:function(evtParam){
        // 이동할 타깃 시트에 따라 원본 시트의 행 처리 방식을 다르게 지정
        if (evtParam.tosheet === Sheet1) return 1;       // 복사 (행 유지)
        else if (evtParam.tosheet === Sheet2) return -1; // 완전 제거
        else return 0;                                   // 삭제 상태로 변경
    }
}
```

### Read More
- [드래그 앤 드롭 이벤트 발생 순서](/docs/events/10-drag-event-flow)
- [CanDrag cfg](/docs/props/cfg/can-drag)
- [DragCopy cfg](/docs/props/cfg/drag-copy)
- [onStartDrag event](./on-start-drag)
- [onEndDrag event](./on-end-drag)
- [onDragFinish event](./on-drag-finish)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
