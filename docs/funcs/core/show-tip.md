# showTip ***(method)***

<!-- synonyms: 풍선도움말, 툴팁, tooltip, 마우스 툴팁, 커서 위치 툴팁, show tip -->

> 현재 마우스 커서가 위치한 곳에 원하는 내용의 풍선도움말을 띄웁니다. `tip` 인자에 HTML 태그를 넣으면 더 다양한 표현도 가능합니다.  
> 셀 오버 시 자동으로 뜨는 툴팁과 달리 명령형 메소드로, 주로 마우스 이벤트(예: `onMouseMove`)에서 호출해 커서 위치에 툴팁을 표시하며 [hideTip](./hide-tip)으로 숨깁니다. 단, 마우스 커서가 **시트 영역 안에 있을 때만** 표시되며 시트 밖에서는 표시되지 않습니다.  
> 셀에 마우스를 올릴 때 자동으로 툴팁을 표시하려면 [(col)Tip](/docs/props/col/tip) 속성이나 [onShowTip](/docs/events/on-show-tip) 이벤트를 사용하세요.

### Syntax
```javascript
void showTip( tip );
```

### Parameters

|Name|Type|Required| Description |
|----------|-----|---|----|
|tip |`string`|<span class='required'>필수</span>|풍선 도움말에 보여질 내용|

### Return Value
***none***

### Example
```javascript
//현재 마우스 커서 위치에 다음 내용을 풍선도움말 형식으로 띄운다.
sheet.showTip("<span style='color:red'>You</span> are so <span style='font-weight:700;color:black'>beautiful</span>");
```

```javascript
// 마우스를 따라 현재 셀 값을 툴팁으로 표시 (자동 셀 툴팁이 아니라 직접 호출)
options.Events = {
    onMouseMove: function (evtParam) {
        if (evtParam.row && evtParam.col) {
            evtParam.sheet.showTip("값: " + evtParam.sheet.getValue({ row: evtParam.row, col: evtParam.col }));
        }
    }
};
```

### Read More

- [hideTip method](./hide-tip)
- [onShowTip event](/docs/events/on-show-tip)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
