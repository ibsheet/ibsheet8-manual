# onBeforeCheckAll ***(event)***

<!-- synonyms: 전체 체크 전, 헤더 체크 확인, 전체 체크 취소, 전체 체크 막기 -->

> 사용자 클릭이나 [setAllCheck](/docs/funcs/core/set-all-check) 호출로 `Bool` 타입 열 전체 체크/체크해제 전에 호출됩니다.  
> `0(false)`를 리턴하면 체크/체크해제가 진행되지 않습니다.  
> 대부분의 이벤트는 `1(true)`를 리턴 시 입력을 무시하는 것과 달리, 이 이벤트는 `false`를 리턴 시 입력을 무시하므로 주의하세요.

### Syntax

```
    onBeforeCheckAll: function(paramObject) {

    }
or
    sheet.bind("onBeforeCheckAll" , function(paramObject) {});
```

### Parameters

| Name | Type | Description |
|----------|-----|-------|
|sheet|`object`|열 전체 체크/체크해제가 될 시트 객체|
|col|`string`|열 전체 체크/체크해제가 될 열이름|

### Return
***boolean*** — `false` 반환 시 전체 체크/체크해제 동작이 취소됩니다.

### Example
```javascript
options.Events = {
    onBeforeCheckAll: function(evtParam) {
        // 사용자 확인 후 진행
        if (!confirm(evtParam.col + " 열의 체크 상태를 변경하시겠습니까?")) {
            return false;
        }
    }
};
```

### Read More
- [체크박스 이벤트 발생 순서](/docs/events/07-check-event-flow)
- [setAllCheck method](/docs/funcs/core/set-all-check)
- [onCheckAllFinish event](./on-check-all-finish)
- [HeaderCheck cfg](/docs/props/cfg/header-check)
- [HeaderCheck col](/docs/props/col/header-check)
- [AllCheckIgnoreEvent col](/docs/props/col/all-check-ignore-event)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.8|기능 추가|
