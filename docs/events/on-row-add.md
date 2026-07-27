# onRowAdd ***(event)***

<!-- synonyms: 행 추가 이벤트, 행 생성, 신규 행, addRow 이벤트, addRows 이벤트, row add, on row add -->

> 시트에 새로운 행이 추가된 직후(렌더링 되기전) 호출되는 이벤트입니다.
>
> [addRow](/docs/funcs/core/add-row), [addRows](/docs/funcs/core/add-rows), [copyRow](/docs/funcs/core/copy-row), [copyRows](/docs/funcs/core/copy-rows) 등 행을 추가하는 메소드 사용 시 호출됩니다(복수 추가 시 추가되는 **행마다**).  
> 단, **붙여넣기(`Ctrl + V`)로 삽입된 행에서는 발생하지 않습니다.** 이 경우 [onAfterRowAdd](/docs/events/on-after-row-add)를 사용하세요.  
> 또한 [addRow](/docs/funcs/core/add-row)를 `render:0`(화면 갱신 안 함)으로 호출하면 발생하지 않습니다.

### Syntax

```
    onRowAdd : function(paramObject) {

    }
or
    sheet.bind("onRowAdd" , function(paramObject) {});
```

### Parameters


| Name | Type | Description |
|----------|-----|-------|
|sheet|`object`|시트 객체|
|row|`object`|시트에 추가될 [데이터 로우 객체](/docs/appx/row-object)|

### Return
***none***


### Example
```javascript
options.Events = {
    onRowAdd:function(evtParam){
        // 행 추가시 여기서 초기값을 설정해줄 수 있습니다.
        // 렌더링을 이 이벤트가 일어난 후 하기 때문에 값만 설정해줘도 반영됩니다.
        evtParam.row["sTitle" ] = "없음";
        evtParam.row["sAudience" ] = 0;
        evtParam.row["sPlace" ] = "미정";
    }
}
```

### Read More

- [addRow method](/docs/funcs/core/add-row)
- [addRows method](/docs/funcs/core/add-rows)
- [copyRow method](/docs/funcs/core/copy-row)
- [copyRows method](/docs/funcs/core/copy-rows)
- [onAfterRowAdd event](./on-after-row-add)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
