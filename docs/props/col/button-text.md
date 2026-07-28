# ButtonText ***(col)***
> [Button](./button)속성의 값이 `Button`이거나 `Html`인 경우, 셀 버튼에 표시할 문자를 설정합니다.
>
> [Button](./button)속성의 값이 `Button`인 경우에는 설정한 문자가 \<u>나 \<button>태그로 표시되며, <br/>`Html`인 경우에는 <span>입력</span>식의 Html 문자가 해석되어 셀에 표시됩니다.


### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`string`|버튼에 들어갈 문자열|

### Example
```javascript
options.Cols = [
    ...
    //셀 우측에 "확인"버튼을 표시한다.
    {Type: "Text", Button: "Button", ButtonText: "확인", Name: "conf_btn", Width: 120, ... },
    ...
    //버튼 타입에 "BTN"버튼을 표시한다.
    { Type: "Button", ButtonText: "BTN", Name: "type_btn", Width: 120, ... },
];
```

### Read More
- [Button col](./button)
- [UseButton cfg](/docs/props/cfg/use-button)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
