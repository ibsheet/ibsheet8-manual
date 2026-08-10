# onShowEditEnum ***(event)***

<!-- synonyms: EditEnum 표시, 편집 열거 리스트, 편집 콤보 리스트, 편집 드롭다운 표시, 편집 리스트 열림, on-show-edit-enum, show edit enum, edit enum list, edit dropdown -->

> [EditEnum](/docs/props/col/edit-enum)타입의 열에서 리스트가 열리기 직전에 호출되는 이벤트입니다.
>
> 새로운 [EditEnum](/docs/props/col/edit-enum) 리스트를 만들고 리턴하여 [EditEnum](/docs/props/col/edit-enum)을 대체해서 사용할 수 있습니다(기존에 [EditEnum](/docs/props/col/edit-enum)이 설정되어 있지 않아도 사용가능 합니다).
>
> 새로운 [EditEnum](/docs/props/col/edit-enum) 리스트를 리턴 시 [Enum](/docs/props/col/enum) 속성에 설정된 리스트의 **개수만큼 설정**해서 리턴해야합니다.

### Syntax

```
    onShowEditEnum : function(paramObject) {

    }
or
    sheet.bind("onShowEditEnum" , function(paramObject) {});
```

### Parameters


| Name | Type | Description |
|----------|-----|-------|
|sheet|`object`|시트 객체|
|row|`object`|`Enum` 리스트가 열리는 [데이터 로우 객체](/docs/appx/row-object)|
|col|`string`|`Enum` 리스트가 열리는열이름|
|editenum|`string`|`EditEnum`에 설정된 값|

### Return
***string***

### Example
```javascript
options.Events = {
    onShowEditEnum:function(evtParam){
        // EditEnum에 "금지어"가 포함된 경우 이를 "좋은말"로 대체해서 화면에 보여줍니다.
        if (evtParam.editenum.indexOf("금지어")) {
            return evtParam.editenum.replace("금지어", "좋은말");
        }
    }
}
```

### Read More

- [Enum col](/docs/props/col/enum)
- [EditEnum col](/docs/props/col/edit-enum)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
