# AddClass ***(col)***

> 열의 Type이 `Button`이고 `Button` 속성의 값이 `Button`인 경우, 버튼에 적용할 CSS Class 명을 설정합니다.
### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`string`|CSS에 정의한 클래스 이름|

### 주의 사항
> - `Class`로 적용한 CSS는 **엑셀 다운로드시 디자인 반영되지 않습니다.**
>
> - 사용자 정의 CSS는 **IBSheet 기본 스타일(main.css) 이후에 로드**해야 적용됩니다.
>   - 순서가 맞지 않으면 `사용자 정의 CSS`가 적용되지 않으며, 불필요하게 `!important`를 사용하게 됩니다.

### Example
```css
<style>

.RedBold{color:#FF0000; font-weight:700;}
</style>
```
```javascript
//특정 열에 "RedBold" 클래스를 적용
options.Cols = [
  
    {Type: "Button", Button: "Button", Name: "sButton", Width: 100},
    // 버튼에 CSS class 적용
    {Type: "Button", Button: "Button", Name: "Dept", AddClass: "RedBold", Width: 100}
    
];

//함수를 이용하여 컬럼에 AddClass적용
sheet.setAttribute({ "col":"sButton", "attr":"AddClass", "val":"RedBold" });

```
### Try it
- [Demo of AddClass](https://jsfiddle.net/gh/get/library/pure/ibsheet/ibsheet8-manual-sample/tree/master/samples/properties/Col/AddClass)

### Read More
- [Button col](/docs/props/col/button)
- [setAttribute method](/docs/funcs/core/set-attribute)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
