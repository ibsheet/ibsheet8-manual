# onShowMenu ***(event)***

<!-- synonyms: 메뉴 표시, 컨텍스트 메뉴 표시, 우클릭 메뉴 열림, 팝업 메뉴 표시, 메뉴 열기, on-show-menu, show menu, context menu show, menu open -->

> 마우스 오른쪽 클릭 시 시트에 설정된 메뉴가 화면에 표시될 때 호출되는 이벤트입니다.  
> `true`를 리턴하면 설정된 메뉴를 표시하지 않습니다.  
> [showMenu](/docs/funcs/core/show-menu) 메소드로 띄운 메뉴에는 호출되지 않습니다.

### Syntax

```
    onShowMenu : function(paramObject) {

    }
or
    sheet.bind("onShowMenu" , function(paramObject) {});
```

### Parameters


| Name | Type | Description |
|----------|-----|-------|
|sheet|`object`|메뉴가 보여질 시트 객체|
|row|`object`|메뉴가 보여질 셀의 [데이터 로우 객체](/docs/appx/row-object)|
|col|`string`|메뉴가 보여질 셀의 열이름|
|menu|`object`|화면에 보여질 메뉴에 대한 설정을 담고 있는 객체|

### Return
***boolean*** : `true`를 리턴하면 해당 메뉴를 화면에 표시하지 않습니다. (리턴값이 없으면 정상 표시)

### Example
```javascript
options.Events = {
    onShowMenu:function(evtParam){
        // 열이름이 preTaskId인 경우 메뉴를 화면에 보여주지 않습니다.
        if (evtParam.col === "preTaskId") return true;
    }
}
```

### Read More
- [Menu appendix](/docs/appx/menu)
- [onSelectMenu event](./on-select-menu)
- [onReadMenu event](./on-read-menu)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
