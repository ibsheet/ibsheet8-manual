# Class ***(col)***

<!-- synonyms: CSS 클래스, 사용자 정의 CSS, 열 스타일, 클래스 지정, css class, custom class, column class, style class, ClassFormula, 클래스 수식, 조건부 클래스, 조건부 CSS, 열 클래스 자동 적용 -->

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

```javascript
// ClassFormula — 조건에 따라 특정 열의 셀 클래스를 자동 지정 (CanFormula, CalcOrder 필요)
options = {
    Def: {
        Row: {CanFormula: 1, CalcOrder: "DeptClass"}  // "열이름 + Class" 형식
    },
    Cols: [
        {Type: "Text", Name: "Dept", Width: 100,
            ClassFormula: function(fr) {
                // Dept 셀 값이 "영업"이면 RedBold 클래스 적용
                if (fr.Row["Dept"] === "영업") return "RedBold";
            }
        }
    ]
};
```

### Try it
- [Demo of Class](https://jsfiddle.net/gh/get/library/pure/ibsheet/ibsheet8-manual-sample/tree/master/samples/properties/Col/Class/)
- [Demo of ClassFormula](https://jsfiddle.net/gh/get/library/pure/ibsheet/ibsheet8-manual-sample/tree/master/samples/properties/Col/ClassFormula/)

### Read More
- [AddClass col](./add-class)
- [setAttribute method](/docs/funcs/core/set-attribute)
- [attribute+Formula col](/docs/props/col/attribute-formula)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
