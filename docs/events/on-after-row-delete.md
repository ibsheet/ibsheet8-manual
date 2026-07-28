# onAfterRowDelete ***(event)***
> [deleteRow](/docs/funcs/core/delete-row), [deleteRows](/docs/funcs/core/delete-rows) 호출 시 행의 삭제 상태 변경 후(렌더링되기 전) 호출되는 이벤트입니다.  
> 시트가 트리구조이고 부모와 자식 행이 모두 삭제 상태로 변경될 경우 자식 행에 대해 먼저 호출됩니다.

### Syntax
```
    onAfterRowDelete : function(paramObject) {

    }
or
    sheet.bind("onAfterRowDelete" , function(paramObject) {});
```

### Parameters
| Name | Type | Description |
|----------|-----|-------|
|sheet|`object`|시트 객체|
|row|`object`|삭제 처리될 행의 [데이터 로우 객체](/docs/appx/row-object)|
|type|`number`|삭제 대상 분류<br/>`1`:행 단위 삭제<br/>`2`:트리/그룹 단위 삭제|

### Return
***none***

### Example
```javascript
options.Events = {
    onAfterRowDelete:function(evtParam){
        alert(evtParam.row.id+"행이 삭제되었습니다.");
    }
}
```

### Read More

- [onBeforeRowDelete event](./on-before-row-delete)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
