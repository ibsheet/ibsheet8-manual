# AllCheckIgnoreEvent ***(col)***

<!-- synonyms: 전체 체크 느림, 헤더 체크 성능, Bool 일괄 체크, onAfterChange 차단, 체크 속도 -->

> 사용자가 헤더 전체 체크박스를 클릭해 전체 체크/체크해제할 때 각 행에서 `onAfterChange` 이벤트 발생 여부를 설정합니다.  
> 행이 많은 시트에서 전체 체크 시 행마다 `onAfterChange`가 호출되어 속도가 저하될 수 있는데, `1`로 설정하면 이벤트가 발생하지 않아 성능이 개선됩니다.  
> 전체 체크 완료 시점에 처리가 필요하면 [onCheckAllFinish](/docs/events/on-check-all-finish) 이벤트를 사용하세요.  
> [setAllCheck](/docs/funcs/core/set-all-check) 메서드 호출 시에는 이 속성이 적용되지 않으므로, 이벤트를 차단하려면 `setAllCheck`의 `ignoreEvent` 인자를 `true`로 지정해야 합니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|`onAfterChange` 이벤트가 발생합니다. (`default`)|
|`1(true)`|`onAfterChange` 이벤트가 발생하지 않습니다.|

### Example
```javascript
// onAfterChange에서 행 색상 변경 등 무거운 로직이 있을 때
// 데이터가 많으면 행마다 호출되어 속도 저하 발생
options.Cols = [
    // AllCheckIgnoreEvent:1 → 전체 체크 시 onAfterChange 발생하지 않음
    {Header: {Value: "주관부서", HeaderCheck: 1}, Type: "Bool", Width: 80, Align: "Center", Name: "ORG_NM", AllCheckIgnoreEvent: 1}
];

options.Events = {
    // 개별 체크 시에만 호출됨 (전체 체크 시 차단)
    onAfterChange: function(evtParam) {
        if (evtParam.col === "ORG_NM") {
            var color = evtParam.val ? "#FFFFCC" : "";
            evtParam.sheet.setAttribute(evtParam.row, null, "Color", color);
        }
    },
    // 전체 체크 완료 시점에 일괄 처리
    onCheckAllFinish: function(evtParam) {
        var rows = evtParam.sheet.getDataRows();
        for (var i = 0; i < rows.length; i++) {
            var color = rows[i]["ORG_NM"] ? "#FFFFCC" : "";
            evtParam.sheet.setAttribute(rows[i], null, "Color", color, 0);
        }
        evtParam.sheet.rerender();
    }
};
```

### Read More
- [HeaderCheck col](/docs/props/col/header-check)
- [setAllCheck method](/docs/funcs/core/set-all-check)
- [onAfterChange event](/docs/events/on-after-change)
- [onCheckAllFinish event](/docs/events/on-check-all-finish)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.15|기능 추가|
