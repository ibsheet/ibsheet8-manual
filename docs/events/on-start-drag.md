# onStartDrag ***(event)***
> 시트 내 행(들)이 드래그되기 전에 호출됩니다.
> 드래그를 취소하거나, 드래그 표시용 HTML을 지정할 수 있습니다.  
> 시트 간 이동 시 이 이벤트는 **드래그 시작 시트에서만 발생**합니다.

<!-- synonyms: row drag start, start row drag, drag start event, 행 드래그 시작, 드래그 이벤트 -->

### Syntax

```
    onStartDrag : function(paramObject) {

    }
or
    sheet.bind("onStartDrag" , function(paramObject) {});
```

### Parameters


| Name | Type | Description |
|----------|-----|-------|
|sheet|`object`|드래그가 시작된 시트 객체|
|row|`object`|단일 행 드래그 시 이동할 행의 [데이터 로우 객체](/docs/appx/row-object)|
|col|`string`|드래그 시작 열 이름|
|more|`boolean`|복수 행 드래그 여부<br/>- 단일 행 드래그: `false`<br/>- 복수 행 드래그: `true`|
|rows|`array[object]`|복수 행 드래그 시 해당 행들의 [데이터 로우 객체](/docs/appx/row-object) 배열|

<!--|copy|`boolean`|복사 여부 (`DragCopy` 설정값에 따라 결정됨)<br/>`0(false)`:이동<br/>`1(true)`:복사| -->


### Return
***mixed(`number` \| `string`)*** 
- `true`를 리턴해도 내부적으로 1과 동일하게 처리됩니다.
- `string`을 리턴하면 기본 Drag UI 대신 해당 HTML이 표시됩니다.

| Return Value | Description |
| -- | -- |
|`1(true)`| 드래그 취소 후 선택 상태 유지 (행 선택 실행)   |
|  `-1`   | 행 드래그 취소 및 이후 동작 모두 취소 |
|`string` | 드래그 표시용 HTML 값으로 대체  |


### Example
```javascript
options.Events = {
    onStartDrag:function(evtParam){
      var sheet = evtParam.sheet;
      
      // 단일 행일 경우 rows 배열이 없으므로 row 객체 사용
      const rowsToCheck = evtParam.rows && evtParam.rows.length ? evtParam.rows : [evtParam.row];

      // 특정 행 조건에서 드래그 취소
      for (let i = 0; i < rowsToCheck.length; i++) {
          const rowData = rowsToCheck[i];
          if(sheet.id === 'LeftSheet' && rowData.sPos === '대표이사'){
              sheet.showMessageTime('대표이사는 이동할 수 없습니다.', 800);
              return true;  // 드래그 취소
          }
      }

    if (evtParam.more) {
      // 복수행일때만 드래그 표시용 HTML
      const firstRow = rowsToCheck[0];
      const count = rowsToCheck.length;

      return `
        <div style="
          padding:8px 12px;
          background:#1976d2;
          color:#fff;
          font-weight:bold;
          border-radius:8px;
          box-shadow:0 4px 10px rgba(0,0,0,0.3);
          white-space:nowrap;
        ">
          ${firstRow.sName} 외 ${count - 1}건 이동
        </div>
      `;
  
      }
    }
}
```

### Try it
- [Demo of onStartDrag](https://jsfiddle.net/gh/get/library/pure/ibsheet/ibsheet8-manual-sample/tree/master/samples/properties/Cfg/CanDrag-true/)

### Read More
- [드래그 앤 드롭 이벤트 발생 순서](/docs/events/10-drag-event-flow)
- [CanDrag cfg](/docs/props/cfg/can-drag)
- [DragCopy cfg](/docs/props/cfg/drag-copy)
- [SelectingCells cfg](/docs/props/cfg/selecting-cells) 
- [onEndDrag event](./on-end-drag)
- [onAfterRowMoveToSheet event](./on-after-row-move-to-sheet)
- [onDragFinish event](./on-drag-finish)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.1.0.1|`-1` 리턴 기능 추가|
|core|8.1.0.14|`string` 리턴 기능 추가|
