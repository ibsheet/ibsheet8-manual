# onSave ***(event)***

<!-- synonyms: 저장 시작, 저장 시도, save start, on save -->

> [doSave](/docs/funcs/core/do-save) 호출 시 가장 먼저 발생하는 이벤트입니다.  
> `1(true)`를 리턴하면 이후 모든 이벤트와 저장 작업이 중단됩니다.

### Syntax

```javascript
options.Events = {
    onSave: function(evtParam) {

    }
};

// 또는
sheet.bind("onSave", function(evtParam) {});
```

### Parameters


| Name | Type | Description |
|----------|-----|-------|
|sheet|`object`|서버에 변경된 내용을 전송할 시트 객체|

### Return
***boolean***

### Example
```javascript
options.Events = {
    onSave:function(evtParam){
        var changes = evtParam.sheet.getChangedData();
        if (changes.indexOf("금지어") > -1) {
            alert("잘못된 문자열이 포함되어 있습니다. 저장을 취소합니다.");
            return true;
        }
    }
}
```

### Read More

- [doSave method](/docs/funcs/core/do-save)
- [저장 응답 규격](/docs/dataStructure/saving-structure)
- [onValidation event](./on-validation)
- [onBeforeSave event](./on-before-save)
- [onAfterSave event](./on-after-save)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
