# onShowEdit ***(event)***

<!-- synonyms: 편집 값 표시, 편집 시작 값, 편집 모드 값 변경, 편집 초기값, 편집 진입 값, on-show-edit, show edit, edit value, edit initial value -->

> 셀 편집 시작 시 편집모드에 보일 값을 가져오기 위해 호출되는 이벤트입니다.
>
> 편집모드를 시작할 때 보일 값 대신 사용될 값을 리턴 할 수 있습니다.

### Syntax

```
    onShowEdit : function(paramObject) {

    }
or
    sheet.bind("onShowEdit" , function(paramObject) {});
```

### Parameters


| Name | Type | Description |
|----------|-----|-------|
|sheet|`object`|편집모드가 시작된 시트 객체|
|row|`object`|편집모드가 시작된 셀이 위치한 [데이터 로우 객체](/docs/appx/row-object)|
|col|`string`|편집모드가 시작된 셀의 열이름|
|val|`string`|편집모드에서 보일 값|

### Return
***string***

### Example
```javascript
options.Events = {
    onShowEdit:function(evtParam){
        // 편집모드의 초기 값을 세팅해줄 수 있다.
        return 1;
    }
}
```

### Read More

- [셀 편집 이벤트 발생 순서](/docs/events/05-edit-event-flow)
- [onStartEdit event](./on-start-edit)
- [onEndEdit event](./on-end-edit)
- [onAfterEdit event](./on-after-edit)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
