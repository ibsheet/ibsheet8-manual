# onBeforeChange ***(event)***

<!-- synonyms: 값 변경 전, 셀 값 수정 전, 값 변경 취소, 값 유효성 검사, on-before-change, before change, value change cancel -->

> 사용자의 입력에 의해 셀의 값이 수정되기 전에 호출되는 이벤트입니다.
>
> `method`를 통한 수정에는 호출되지 않습니다.
>
> 기존의 값과 동일한 값으로 수정되었을 경우에도 발생합니다.
>
> `return Value`: 변경할 값을 리턴시 사용자 입력과 무관하게 변경된 내용이 셀에 셋팅 됩니다. 
>
> `return null`: 사용자가 입력한 값이 적용됩니다.

### Syntax

```
    onBeforeChange : function(paramObject) {

    }
or
    sheet.bind("onBeforeChange" , function(paramObject) {});
```

### Parameters
| Name | Type | Description |
|----------|-----|-------|
|sheet|`object`|값 변경이 일어난 시트 객체|
|row |`object`|[데이터 로우 객체](/docs/appx/row-object)|
|col |`string`|열이름|
|val |`number` \| `string` \| `object`|변경하려는 값|
|oldval|`number` \| `string` \| `object`|변경하기 이전값|
<!--!
|`[비공개]` error|`object`|[이벤트 error 객체](/docs/appx/event-error)| 
!-->

### Return Value
***string***

### Example
```javascript
options.Events = {
    onBeforeChange:function(evtParam){
        // 값 수정 전 이벤트 로직.
        if(evtParam.col == "AMT" && evtParam.val > 2000){
            alert("최대 설정 값은 2000까지 입니다.");
            return evtParam.oldval;
        } else {
            return null;
        }
    }
}
```

### Read More

- [셀 편집 이벤트 발생 순서](/docs/events/05-edit-event-flow)
- [onAfterChange event](./on-after-change)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
