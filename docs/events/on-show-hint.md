# onShowHint ***(event)***

<!-- synonyms: 힌트 표시, 힌트 값 변경, 커스텀 힌트, hint 표시, 셀 힌트, on-show-hint, show hint, custom hint, hint display -->

> 힌트가 화면에 보여질 때 호출되는 이벤트입니다.  
> 힌트 값을 변경하고 싶은 경우, 사용자가 원하는 커스텀 `hint` 값(기본은 셀 값)을 리턴합니다.  
> 기본적으로 셀 내용이 잘려 힌트가 표시될 때만 호출되며, 내용이 잘리지 않은 셀에서도 호출되게 하려면 [ShowHint](/docs/props/col/show-hint)를 `3`으로 설정합니다.

### Syntax

```
    onShowHint : function(paramObject) {

    }
or
    sheet.bind("onShowHint" , function(paramObject) {});
```

### Parameters


| Name | Type | Description |
|----------|-----|-------|
|sheet|`object`|힌트가 보여질 시트 객체|
|row|`object`|힌트가 보여질 셀의 [데이터 로우 객체](/docs/appx/row-object)|
|col|`string`|힌트가 보여질 셀의 열이름|
|hint|`string`|화면에 보여질 힌트 값|
|reason|`number`|힌트가 보이게 된 원인<br/>`0`:셀 내용이 잘리지 않았을 때([ShowHint](/docs/props/col/show-hint)가 `3`인 경우)<br/>`1`:셀 내용의 너비가 셀의 너비보다 클 때<br/>`2`:셀 내용의 높이가 셀의 높이보다 클 때<br/>`3`:셀 내용의 너비/높이가 셀의 너비/높이보다 클 때|

### Return
***string*** : 리턴한 값이 힌트 내용으로 표시됩니다. 리턴하지 않으면 원래 힌트 값(기본은 셀 값)이 그대로 표시되고, 빈 문자열(`""`)을 리턴하면 힌트가 표시되지 않습니다.

### Example
```javascript
options.Cols = [
    // ShowHint: 3 이면 내용이 잘리지 않은 셀에서도 onShowHint 가 호출됨
    {Type: "Text", Name: "sTitle", Width: 100, ShowHint: 3},
    {Type: "Text", Name: "STATE", Width: 80}
];
options.Events = {
    onShowHint: function(evtParam) {
        if (evtParam.col != "sTitle") return;            // 다른 열은 원래 힌트 그대로
        if (evtParam.row["STATE"] == "마감") {
            return "마감된 건입니다.";                    // 셀 내용 대신 안내 문구 표시
        }
        if (evtParam.reason == 0) return "";              // 내용이 잘리지 않은 셀은 힌트 표시 안 함
    }
};
```

### Read More
- [ShowHint col](/docs/props/col/show-hint)
- [HintValue cell](/docs/props/cell/hint-value)
- [HintValue col](/docs/props/col/hint-value)
- [HintValue row](/docs/props/row/hint-value)
- [showHint method](/docs/funcs/core/show-hint)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
