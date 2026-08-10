# NoButtonInFilter ***(col)***

<!-- synonyms: 필터행 버튼 제거, 필터 버튼 숨김, 필터 TimePicker 숨김, 필터 셀 정리, no button filter, filter row button hide, hide filter button -->

> 해당 열의 필터행에 [Button](./button), [TimePicker](./time-picker) 을 통해 생성되는 `Button` 혹은 `TimePicker` 가 생성되지 않도록 합니다.


### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|필터행에 `Button` 혹은 `TimePicker` 생성됨 (`default`)|
|`1(true)`|필터행에 `Button` 혹은 `TimePicker` 생성되지 않음|

### Example
```javascript
// 특정 열의 필터행에 버튼이 생성되지 않도록 설정
options.Cols = [
    {Type: "Text", Button: "Button", ButtonText: "TestButton", Name: "sNumber", NoButtonInFilter: 1, Width: 70 ...},
    ...
];
```

### Read More
- [Button](./button)
- [TimePicker](./time-picker)

### Since

|product|version|desc|
|---|---|---|
|core|8.1.0.76|기능 추가|