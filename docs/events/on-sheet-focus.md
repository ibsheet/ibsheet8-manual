# onSheetFocus ***(event)***
> 시트에 포커스 되었을때 호출되는 이벤트입니다.

### Syntax

```
    onSheetFocus : function(paramObject) {

    }
or
    sheet.bind("onSheetFocus" , function(paramObject) {});
```

### Parameters
| Name | Type | Description |
|----------|-----|-------|
|sheet|`object`|포커스가 된 시트 객체|

### Return
***none***


### Example
```javascript
options.Events = {
    onSheetFocus:function(evtParam){
        alert("현재 포커스된 시트는 "+evtParam.sheet.id+" 입니다.");
    }
}
```

### Read More
- [onFocus event](/docs/events/on-focus)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.7|기능 추가|
