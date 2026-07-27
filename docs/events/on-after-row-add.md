# onAfterRowAdd ***(event)***

<!-- synonyms: 행 추가 후 이벤트, 다중 행 추가, addRows 이벤트, copyRows 이벤트, 붙여넣기 행 추가, after row add -->

> 시트에 새로운 행이 추가되어 렌더링된 후 호출되는 이벤트입니다.
>
> [addRows](/docs/funcs/core/add-rows), [copyRows](/docs/funcs/core/copy-rows), 또는 붙여넣기(`Ctrl + V`)로 여러 행을 한 번에 추가할 때 추가되는 **행마다** 호출됩니다.  
> 단일 행 추가([addRow](/docs/funcs/core/add-row), [copyRow](/docs/funcs/core/copy-row))에서는 발생하지 않습니다.

### Syntax
```
    onAfterRowAdd : function(paramObject) {

    }
or
    sheet.bind("onAfterRowAdd" , function(paramObject) {});
```

### Parameters
| Name | Type | Description |
|----------|-----|-------|
|sheet|`object`|시트 객체|
|row|`object`|시트에 추가된 [데이터 로우 객체](/docs/appx/row-object)|

### Return
***none***

### Example
```javascript
options.Events = {
    onAfterRowAdd:function(evtParam){
        // 행 추가시 여기서 초기값을 설정해줄 수 있습니다.
        // 렌더링 된 후 호출되는 이벤트이기에 값 변경시 렌더링을 해줘야합니다.
        evtParam.sheet.setValue({row:evtParam.row,col:"sTitle",val:"없음",render:1});
        evtParam.sheet.setValue({row:evtParam.row,col:"sAudience",val:0,render:1});
        evtParam.sheet.setValue({row:evtParam.row,col:"sPlace",val:"미정",render:1});
    }
}
```

### Read More
- [addRows method](/docs/funcs/core/add-rows)
- [copyRows method](/docs/funcs/core/copy-rows)
- [onRowAdd event](./on-row-add)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
