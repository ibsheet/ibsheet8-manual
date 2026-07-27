# SyncCalcOnAfterChange ***(cfg)***

> [onAfterChange](/docs/events/on-after-change) 이벤트에서 설정된 합계, 소계 값을 즉시 재계산하여 반환하는 설정입니다.<br/>
> 기본적으로 여러 셀을 한번에 수정하는 경우 `onAfterChange`에서 합계, 소계가 아직 재계산되지 않은 값이 반환됩니다.<br/>
> `true`로 설정하면 매 셀 `onAfterChange`마다 합계, 소계를 재계산하여 변경된 소계값을 확인할 수 있습니다.<br/>
> `주의: true 설정 시 매 셀마다 합계, 소계를 재계산하므로 다중 셀 수정 시 성능이 저하될 수 있습니다.`


### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|`onAfterChange`에서 소계를 재계산하지 않음 (`default`)|
|`1(true)`|`onAfterChange`에서 매 셀마다 소계를 즉시 재계산하여 반환|

### Example
```javascript
options.Cfg = {
    SyncCalcOnAfterChange: true
};

options.Event = {
    onAfterChange: function(evt) {
        // 변경된 소계값을 바로 확인 가능
        console.log(sheet.SubSumRowsArray[0].SubSumRow.A);
    }
};
```

### Read More
- [onAfterChange event](/docs/events/on-after-change)

### Since

|product|version|desc|
|---|---|---|
|core|8.3.0.62|기능 추가|
