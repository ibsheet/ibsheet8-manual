# SpinnerMax ***(col)***

<!-- synonyms: 스피너 최댓값, 스피너 최대값, 숫자 최대, 증감 최대, spinner max, max value, number max, spinner upper limit -->

> [SpinnerVisible](./spinner-visible)을 사용하는 열에서 화살표를 통한 입력 시 최댓값을 설정할 수 있습니다.
>
> 
>
> 추가적으로 [SpinnerStep](./spinner-step), [SpinnerMin](./spinner-min)을 통해 input의 step, min를 설정 할 수 있습니다. 

### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`number`|편집 시 입력 값의 최댓값|


### Example
```javascript
options.Cols = [
    ...
    {Type: "Int", Name: "Qty", SpinnerVisible: true, SpinnerMax: 100000, ...},
    ...
];
```

### Read More
- [Type appendix](/docs/appx/type)
- [SpinnerVisible](./spinner-visible)
- [SpinnerStep](./spinner-step)
- [SpinnerMin](./spinner-min)

### Since

|product|version|desc|
|---|---|---|
|core|8.1.0.88|기능 추가|
