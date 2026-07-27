# onCheckAllFinish ***(event)***

<!-- synonyms: 전체 체크 완료, 헤더 체크 후 처리, 일괄 체크 완료, 체크 후 일괄 처리 -->

> 사용자가 헤더 전체 체크박스를 클릭하거나 [setAllCheck](/docs/funcs/core/set-all-check) 호출로 `Bool` 타입 열 전체 체크/체크해제가 완료된 후 호출됩니다.  
> [AllCheckIgnoreEvent](/docs/props/col/all-check-ignore-event)`:1`로 `onAfterChange`를 차단하고 전체 체크 후 일괄 처리하는 패턴에 자주 사용됩니다.

### Syntax
```
    onCheckAllFinish: function(paramObject) {

    }
or
    sheet.bind("onCheckAllFinish" , function(paramObject) {});
```

### Parameters
| Name | Type | Description |
|----------|-----|-------|
|sheet | `object` | 전체 체크/체크해제가 완료된 시트 객체 |
|col | `string` | 전체 체크/체크해제가 완료된 열이름 |
|result | `boolean` | 체크 여부<br>`0(false)`: 체크해제<br>`1(true)`: 체크 |

### Return
***none***

### Example
```javascript
options.Events = {
    onCheckAllFinish: function(evtParam) {
        var state = evtParam.result ? "체크" : "체크해제";
        alert(evtParam.col + " 열이 전체 " + state + " 완료되었습니다.");
    }
};
```

### Read More
- [체크박스 이벤트 발생 순서](/docs/events/07-check-event-flow)
- [setAllCheck method](/docs/funcs/core/set-all-check)
- [onBeforeCheckAll event](./on-before-check-all)
- [HeaderCheck cfg](/docs/props/cfg/header-check)
- [HeaderCheck col](/docs/props/col/header-check)
- [AllCheckIgnoreEvent col](/docs/props/col/all-check-ignore-event)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.8|기능 추가|
