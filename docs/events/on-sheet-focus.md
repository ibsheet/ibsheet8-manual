# onSheetFocus ***(event)***

<!-- synonyms: 시트 포커스, 시트 활성화, 시트 클릭, 시트 선택, 포커스 이동, on-sheet-focus, sheet focus, focus sheet, activate sheet -->

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
