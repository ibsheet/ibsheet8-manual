# onAfterChange ***(event)***

<!-- synonyms: 값 변경 후, 셀 값 변경 완료, 값 변경 이후, 셀 데이터 변경 후, on-after-change, after change, value changed, cell changed -->

> 사용자의 입력에 의해 셀의 값이 수정된 후 호출되는 이벤트입니다.
>
> `method`를 통한 수정에는 호출되지 않습니다.
>
> 기존의 값과 동일한 값으로 수정되었을 경우에도 호출되지 않습니다.

### Syntax

```
    onAfterChange : function(paramObject) {

    }
or
    sheet.bind("onAfterChange" , function(paramObject) {});
```

### Parameters


| Name | Type | Description |
|----------|-----|-------|
|sheet|`object`|값 변경이 일어난 시트 객체|
|row |`object`|[데이터 행 객체](/docs/appx/row-object)|
|col |`string`|열이름|
|val |`number` \| `string` \| `object`|변경된 값|

### Return
***none***


### Example
```javascript
options.Events = {
    onAfterChange:function(evtParam){
        // 값 수정 후 이벤트 로직.
        alert("셀 값이 " + evtParam.val + "로 변경되었습니다.");
    }
}
```

### Read More

- [셀 편집 이벤트 발생 순서](/docs/events/05-edit-event-flow)
- [onBeforeChange event](./on-before-change)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
