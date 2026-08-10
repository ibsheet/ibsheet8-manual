# onShowTip ***(event)***

<!-- synonyms: 풍선도움말, 툴팁 표시, tip 표시, 풍선도움말 표시, 도움말 표시, 셀 도움말, on-show-tip, show tip, tooltip, balloon tip -->

> 시트의 셀 내부에 마우스 커서를 위치 시 풍선도움말이 화면에 띄워질 때 호출되는 이벤트입니다.
>
> 시트에 [Tip](/docs/props/row/tip)이 설정되어있지 않아도 **이 이벤트는 항상 발생합니다**.
>
> 풍선도움말의 값을 바꾸고 싶은 경우, 사용자가 원하는 문자열을 리턴하면 해당 문자열이 풍선도움말의 값으로 변경되어 보여집니다.
>
> 사용자가 리턴할 문자열에 \*Value\*을 포함하면 셀 값이 \*Value\* 자리에 치환되어 풍선도움말에 표시됩니다.
>
> 빈 문자열("")을 리턴 시 풍선도움말을 화면에 보여주지 않습니다.

### Syntax

```
    onShowTip : function(paramObject) {

    }
or
    sheet.bind("onShowTip" , function(paramObject) {});
```

### Parameters


| Name | Type | Description |
|----------|-----|-------|
|sheet|`object`|풍선도움말이 보여질 시트 객체|
|row|`object`|풍선도움말이 보여질 셀의 [데이터 로우 객체](/docs/appx/row-object)|
|col|`string`|풍선도움말이 보여질 셀의 열이름|
|tip|`string`|풍선도움말에 보여질 값|
|clientX|`number`|이벤트가 발생된 마우스의 x좌표(브라우저 기준)|
|clientY|`number`|이벤트가 발생된 마우스의 y좌표(브라우저 기준)|
|X|`number`|이벤트가 발생된 마우스의 x좌표(셀 기준)|
|Y|`number`|이벤트가 발생된 마우스의 y좌표(셀 기준)|

### Return
***string***

### Example
```javascript
options.Events = {
    onShowTip:function(evtParam){
        // 풍선도움말의 값을 열마다 다르게 보여줍니다.
        if(evtParam.col == "sTitle") {
            return "영화 이름은 *Value*입니다!";
        } else if (evtParam.col == "sNum") {
            return "*Value*명의 관객이 영화를 보았습니다";
        }
    }
}
```

### Read More

- [Tip col](/docs/props/col/tip)
- [showTip method](/docs/funcs/core/show-tip)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
