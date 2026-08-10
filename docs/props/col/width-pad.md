# WidthPad ***(col)***

<!-- synonyms: 우측 버튼 너비, 버튼 패드 너비, 셀 버튼 폭, width pad, button pad width, right button width, cell button pad -->

> [Button](./button)속성을 이용하여 셀 우측에 작은 버튼을 표시할때 버튼의 너비를 설정합니다.
>
> 너비는 pixel단위로 설정됩니다.



### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`number`|우측 버튼의 너비(default : 25px)|

### Example
```javascript
options.Cols = [
    ...
    //셀 우측에 "확인"버튼을 표시한다.
    {Type: "Text", Button: "Button", ButtonText: "확인", WidthPad: 25, Name: "conf_btn", Width: 120, ...},
    ...
];
```

### Read More
- [Button col](./button)
- [UseButton cfg](/docs/props/cfg/use-button)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
