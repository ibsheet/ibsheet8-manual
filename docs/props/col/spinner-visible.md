# SpinnerVisible ***(col)***

<!-- synonyms: 스피너, 증감 화살표, 숫자 스피너, 날짜 스피너, spinner, date spinner, 화살표 -->

> [Type](/docs/appx/type)이 `Int`, `Float`, `Date`인 열에서 편집 시 증감 화살표(스피너)를 표시합니다.
>
> `Int`, `Float`인 경우 [SpinnerStep](./spinner-step), [SpinnerMax](./spinner-max), [SpinnerMin](./spinner-min)을 통해 증감 간격과 최솟값/최댓값을 설정할 수 있습니다.
>
> `Date`인 경우 [SpinnerField](./spinner-field)에 `y`, `M`, `d`, `H`, `m`, `s` 중 하나를 지정해 증감 단위(년/월/일/시/분/초)를 설정할 수 있습니다. 지정하지 않으면 `d`(일)가 기본값입니다.
>
> `제약사항` [EditMaskFunc](../cfg/edit-mask-func)가 적용된 열에서는 동작하지 않습니다.

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
    // Int / Float 열 — 숫자 스피너
    {Type: "Int", Name: "Qty", SpinnerVisible: true, SpinnerStep: 10},

    // Date 열 — 날짜 스피너 (월 단위 증감)
    {Type: "Date", Name: "OrderDate", SpinnerVisible: true, SpinnerField: "M"},
    ...
];
```

### Read More
- [Type appendix](/docs/appx/type)
- [SpinnerField col](./spinner-field)
- [SpinnerStep col](./spinner-step)
- [SpinnerMax col](./spinner-max)
- [SpinnerMin col](./spinner-min)
- [SpinnerVisible cell](/docs/props/cell/spinner-visible)

### Since

|product|version|desc|
|---|---|---|
|core|8.1.0.88|기능 추가|
|core|8.4.0.4|`Type:Date` 열에서도 스피너 표시 지원|
