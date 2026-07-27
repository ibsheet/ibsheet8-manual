# UseDefaultTime ***(cfg)***

<!-- synonyms: 기본 시각, 현재 시각 자동 입력, 시간 자동, 시간 포맷 기본값, default time, current time -->

> [Type](/docs/appx/type)이 `Date`이고 [Format](/docs/props/col/format)이 시간 단위(`h`, `m`, `s`)만 포함하는 셀에서, 빈 셀의 편집을 시작할 때 현재 시각을 기본값으로 채워줍니다.  
> Format에 날짜 단위(`y`, `M`, `d`, `D`)가 포함된 경우에는 적용되지 않습니다. 즉 `hh:mm:ss`, `hh:mm`, `mm:ss` 같은 시간 전용 포맷에서만 동작합니다.  
> 이미 값이 있는 셀에는 적용되지 않으며, 편집을 시작하는 시점에 적용됩니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|빈 시간 셀 편집 시 기본값을 채우지 않음 (`default`)|
|`1(true)`|빈 시간 셀 편집 시 현재 시각을 기본값으로 채움|

### Example
```javascript
options.Cfg = {
    UseDefaultTime: 1
};

options.Cols = [
    // 시간 전용 포맷 — 편집 시작 시 현재 시각이 자동으로 채워짐
    {Type: "Date", Name: "StartTime", Format: "hh:mm:ss"},

    // 날짜가 포함된 포맷 — 영향 없음
    {Type: "Date", Name: "OrderDate", Format: "yyyy-MM-dd"}
];
```

### Read More
- [Type appendix](/docs/appx/type)
- [Format col](/docs/props/col/format)
- [onStartEdit event](/docs/events/on-start-edit)

### Since

|product|version|desc|
|---|---|---|
|core|8.4.0.9|기능 추가|
