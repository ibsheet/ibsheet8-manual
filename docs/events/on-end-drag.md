# onEndDrag ***(event)***
> 드래그된 행(들)이 드랍되는 시점에 호출되는 이벤트입니다.  
> 리턴 값에 따라 드래그 드랍을 허용하거나 거부하고,  
> 드랍될 위치를 지정할 수 있습니다.  
> 시트 간 이동 시 이 이벤트는 **드래그 시작 시트에서만 발생**합니다.

<!-- synonyms: end drag, row drop, drag end event, 드래그 종료, 행 드랍 이벤트 -->

### Syntax

```
    onEndDrag : function(paramObject) {

    }
or
    sheet.bind("onEndDrag" , function(paramObject) {});
```

### Parameters
| Name | Type | Description |
|----------|-----|-------|
|sheet|`object`|드래그가 시작된 시트 객체|
|row|`object`|단일 행 드래그 시 이동할 행의 [데이터 로우 객체](/docs/appx/row-object)|
|tosheet|`object`|행이 이동할 대상 시트 객체|
|torow|`object`|드랍될 위치 기준의 [데이터 로우 객체](/docs/appx/row-object)|
|type|`number`|드래그 드랍 허용 여부 및 드랍 위치 정보<br/>`0`:드래그 드랍 불가<br/>`1`:`torow` [데이터 로우 객체](/docs/appx/row-object)의 위쪽에 드랍(드랍될 시트의 데이터가 없을 경우도 이에 해당)<br/>`2`: 이동한 대상 시트가 트리/그룹인 경우 `torow` [데이터 로우 객체](/docs/appx/row-object)의 하위 노드에(자식) 드랍<br/>`3`:`torow` [데이터 로우 객체](/docs/appx/row-object)의 아래쪽에 드랍<br/>`4`: 시트 외부 영역에 드랍|
|x|`number`|드랍 시 마우스 커서 x좌표(브라우저 기준)|
|y|`number`|드랍 시 마우스 커서 y좌표(브라우저 기준)|
|rows|`array[object]`|복수 행 드래그 시 이동 대상 행들의 [데이터 로우 객체](/docs/appx/row-object) 배열|

<!--|copy|`boolean`|복사 여부 (`DragCopy` 설정값에 따라 결정됨)<br/>`0(false)`:이동<br/>`1(true)`:복사| -->

### Return
***number***

- 리턴 값에 따라 드랍 동작이 결정됩니다.  
- 값을 리턴하지 않으면 기본 드래그 드랍 동작이 그대로 수행됩니다.  
- 드랍을 취소하거나 위치를 변경하고 싶을 때만 값을 리턴합니다.

| Return Value | Description                  |
| ------------ | ---------------------------- |
| `0`          | 드래그 드랍 취소                    |
| `1`          | `torow` 위쪽에 드랍               |
| `2`          | `torow` 하위 노드로 드랍 (트리/그룹 시트) |
| `3`          | `torow` 아래쪽에 드랍              |
| `4`          | 시트 외부 영역에 드랍                 |

### Example
```javascript
options.Events = {
    onEndDrag:function(evtParam){
        // 다른 시트로 이동하는 경우만 검사
      if (evtParam.sheet !== evtParam.tosheet) {

        // 복수행 드래그인 경우만 처리
        var rowsToCheck = evtParam.rows && evtParam.rows.length
        ? evtParam.rows
        : evtParam.row
          ? [evtParam.row]
          : [];

        var blocked = false;
        for (var i = rowsToCheck.length - 1; i >= 0; i--) {

          var moveRow = rowsToCheck[i];

          // 여기서 개별 행마다 체크
          if (
            moveRow.sName === "김미경" &&
            evtParam.torow &&
            evtParam.torow.deptId &&
            evtParam.torow.deptId.startsWith("SALES")
          ) {

            blocked = true;
            
            setTimeout(function(){
              evtParam.sheet.showMessageTime(
                "김미경은 영업부서로 이동할 수 없습니다.",
                800
              );
            },10);
            
            // 복수 드래그일 경우 실제 배열 제거
            if (evtParam.rows && evtParam.rows.length) {
              evtParam.rows.splice(i, 1);
            } else {
              // 단일 드래그면 전체 취소
              return 0;
            }
          }
        }
      }
    }
}
```

- [Demo of onEndDrag](https://jsfiddle.net/gh/get/library/pure/ibsheet/ibsheet8-manual-sample/tree/master/samples/properties/Cfg/CanDrag-true/)

### Read More

- [드래그 앤 드롭 이벤트 발생 순서](/docs/events/10-drag-event-flow)
- [CanDrag cfg](/docs/props/cfg/can-drag)
- [DragCopy cfg](/docs/props/cfg/drag-copy)
- [onStartDrag event](./on-start-drag)
- [onAfterRowMoveToSheet event](./on-after-row-move-to-sheet)
- [onDragFinish event](./on-drag-finish)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.3.0.28|type:4 기능 추가|
