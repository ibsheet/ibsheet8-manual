# onRowLoad ***(event)***

<!-- synonyms: 행 로드, 로우 로드, 행 생성, 행 객체 생성, 데이터 로드 시 행, 조회 시 행마다, on-row-load, row load, row created, row loaded -->

> 데이터 조회 시 [데이터 로우 객체](/docs/appx/row-object)가 생성된 직후 호출되는 이벤트입니다.
>
> 시트의 렌더링이 완료되기전 시트에 생성되는 각 행마다 호출되며, 해당 이벤트에서 행의 속성 또는 행에 있는 셀의 데이터를 변경할 수 있습니다.
>
> 해당 이벤트 내에서 **[addRow](/docs/funcs/core/add-row) 메소드를 통해 시트에 새로운 행을 추가 할 수 없습니다.** 
>
> 해당 이벤트 내에서 **[setValue](/docs/funcs/core/set-value) 메소드로 데이터를 변경하는 경우 `calc:0` 인자를 사용해야 합니다.** 
>
> 해당 이벤트 내에서 **[setRowValue](/docs/funcs/core/set-row-value) 메소드로 데이터를 변경하는 경우 `render:0`, `calc:0` 인자를 사용해야 합니다.**
>
> **<mark>주의</mark>** : 행마다 호출되므로 조회 성능이 떨어지므로 이 이벤트 사용은 권장하지 않습니다. 

### Syntax

```
    onRowLoad : function(paramObject) {

    }
or
    sheet.bind("onRowLoad" , function(paramObject) {});
```

### Parameters


| Name | Type | Description |
|----------|-----|-------|
|sheet|`object`|렌더링을 진행할 시트 객체|
|row|`object`|시트에 추가될 [데이터 로우 객체](/docs/appx/row-object)|
|eventName|`string`|이벤트 이름|

### Return
***boolean***

### Example
```javascript
options.Events = {
    onRowLoad:function(evtParam){
        // 행의 CUST_CD 열이름에 해당하는 셀 값이 500이상인 경우 셀 내 텍스트 컬러를 빨간색으로 변경합니다.
        if (evtParam.row["CUST_CD"] >= 500) {
            evtParam.row["CUST_CD"+"TextColor"] = "#FF0000";
        }
    }
}
```

### Read More
- [조회 이벤트 발생 순서](/docs/events/02-search-event-flow)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
