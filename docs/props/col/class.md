# Class ***(col)***

> 열에 적용할 `사용자 정의 CSS`를 설정합니다.
>
> `Type : "Button"`은 내부 구조상 `Class` 속성이 적용되지 않으므로, [AddClass](./add-class) 속성을 사용해야 합니다.

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
/* 글자를 빨간색, 볼드로 표시 */
.RedBold{color:#FF0000; font-weight:700}
</style>
```
```javascript

//1. 특정 열(Dept)에 "RedBold" 클래스를 적용
options.Cols = [
    
    {Type: "Text", Name: "Dept", Class: "RedBold", Width: 100},
    {Type: "Text", Name: "sName", Width: 150 }
];

//2. 함수를 이용하여 CSS 적용
sheet.setAttribute({ "col" :"Dept" ,"attr":"Class", "val":"RedBold" });

```
### Try it
- [Demo of Class](https://jsfiddle.net/gh/get/library/pure/ibsheet/ibsheet8-manual-sample/tree/master/samples/properties/Col/Class/)
- [Demo of ClassForm](https://jsfiddle.net/gh/get/library/pure/ibsheet/ibsheet8-manual-sample/tree/master/samples/properties/Col/ClassFormula/)
- 
### Read More
- [AddClass col](./add-class)
- [setAttribute method](/docs/funcs/core/set-attribute)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
