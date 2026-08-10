# ButtonWidth ***(col)***

<!-- synonyms: 버튼 너비, 버튼 폭, 버튼 크기, 셀 버튼 사이즈, button width, button size, cell button width -->

> [Type](/docs/appx/type)이 `Button`이고, [Button](./button)속성의 값이 `Button`인 경우, 셀에 생성되는 버튼 객체의 너비를 설정합니다.


### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`number`|버튼 객체의 너비|

### Example
```javascript
//버튼의 너비를 80px로 설정
options.Cols = [
    ...
    {Type: "Button", Button: "Button", Name: "btn1", ButtonWidth: 80 ...},
    ...
];
```

### Read More
- [Button col](./button)



### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
