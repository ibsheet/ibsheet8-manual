# SpinnerStep ***(cell)***

<!-- synonyms: 스피너 스텝, 증감 간격, 증가 단위, 감소 단위, 증분, 증감폭, 스피너 단위, 화살표 증감, spinner step, step value, increment, delta, stride -->

> [SpinnerVisible](./spinner-visible)을 사용하는 셀에서 입력 값의 증감 간격을 설정할 수 있습니다.
>
> 
>
> 추가적으로 [SpinnerMax](./spinner-max), [SpinnerMax](./spinner-min)을 통해 input의 min, max를 설정 할 수 있습니다. 

### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`number`|편집 시 입력 값의 증감 간격|


### Example
```javascript
options.cells = [
    ...
    {Type: "Int", Name: "Qty", SpinnerVisible: true},
    ...
];

var data = [
    {Qty: 10, QtySpinnerStep: 10},
    {Qty: 20, QtySpinnerStep: 20},
]
```

### Read More
- [Type appendix](/docs/appx/type)
- [SpinnerVisible](./spinner-visible)
- [SpinnerMax](./spinner-max)
- [SpinnerMin](./spinner-min)

### Since

|product|version|desc|
|---|---|---|
|core|8.3.0.42|기능 추가|
