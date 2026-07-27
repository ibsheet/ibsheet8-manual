# SpinnerVisible ***(cell)***

<!-- synonyms: 스피너, 증감 화살표, 숫자 스피너, 날짜 스피너, spinner, date spinner, 화살표 -->

> [Type](/docs/appx/type)이 `Int`, `Float`, `Date`인 셀에서 편집 시 증감 화살표(스피너)를 표시합니다.
>
> `Int`, `Float`인 경우 [SpinnerStep](./spinner-step), [SpinnerMax](./spinner-max), [SpinnerMin](./spinner-min)을 통해 증감 간격과 최솟값/최댓값을 설정할 수 있습니다.
>
> `Date`인 경우 [SpinnerField](./spinner-field)에 `y`, `M`, `d`, `H`, `m`, `s` 중 하나를 지정해 증감 단위(년/월/일/시/분/초)를 설정할 수 있습니다. 지정하지 않으면 `d`(일)가 기본값입니다.
>
> `제약사항` [EditMaskFunc](../cfg/edit-mask-func)가 적용된 셀에서는 동작하지 않습니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|편집 시 증감 화살표를 표시하지 않음 (`default`)|
|`1(true)`|편집 시 증감 화살표를 표시|

### Example
```javascript
options.Cols = [
    ...
    {Type: "Int", Name: "Qty", SpinnerVisible: false},
    {Type: "Date", Name: "OrderDate"},
    ...
];

// 데이터 단위로 특정 셀에서만 스피너 활성화/비활성화
var data = [
    {Qty: 10, QtySpinnerVisible: true, OrderDate: "2026-05-29", OrderDateSpinnerVisible: true, OrderDateSpinnerField: "M"},
    {Qty: 20, QtySpinnerVisible: false}
];
```

### Read More
- [Type appendix](/docs/appx/type)
- [SpinnerField cell](./spinner-field)
- [SpinnerStep cell](./spinner-step)
- [SpinnerMax cell](./spinner-max)
- [SpinnerMin cell](./spinner-min)
- [SpinnerVisible col](/docs/props/col/spinner-visible)

### Since

|product|version|desc|
|---|---|---|
|core|8.3.0.42|기능 추가|
|core|8.4.0.4|`Type:Date` 셀에서도 스피너 표시 지원|
