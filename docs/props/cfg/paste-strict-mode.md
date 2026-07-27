# PasteStrictMode ***(cfg)***

> `ctrl+v` 를 통해 클립보드의 내용을 시트에 붙여넣을 때, 타입에 맞는 데이터만 붙여넣기 하는 것을 허용할 지 여부를 설정합니다.
>
> `Int`, `Float` 타입의 컬럼에 대해서 붙여넣기 할때, 숫자인지 엄격하게 검사합니다.
>
> 천단위 구분 쉼표는 허용합니다.
>
> `ibsheet-common.js (1.0.14-20241219-14)` 사용하실 경우 기본 값은 `1(true)` 로 설정 됩니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|숫자 데이터에 대해 정밀 검사하지 않음 (`default`)|
|`1(true)`|숫자 데이터가 아닐 경우 붙여넣기 Skip.|


### Example
```javascript
options.Cfg = {
    PasteStrictMode: 1
};
```

### Read More
[onAfterPaste event](/docs/events/on-after-paste)

### Since

|product|version|desc|
|---|---|---|
|core|8.2.0.13|기능 추가|
