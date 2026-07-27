# Class ***(cell)***

> 셀에 적용할 `사용자 정의 CSS`를 설정합니다.

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
.RedBold{color:#FF0000; font-weight:700;}
</style>
```
```javascript
//1. 데이터 행객체(예: AR10)에 직접 접근하여 셀에 CSS 적용
var ROW = sheet.getRowById("AR10");
ROW["CLSClass"] = "RedBold";
//변경내용 반영
sheet.refreshCell({row:ROW, col:"CLS"});

//2. 함수를 이용하여 셀에 CSS 적용
var row = sheet.getRowById("AR1");
sheet.setAttribute({ "row" :row ,"col":"CLS", "attr":"Class", "val":"RedBold" });

//3. 조회 데이터 내에서 속성설정(열이름이 CLS 로 가정)
{
    data:[
        {... , "CLSClass":"RedBold" , ...}
    ]
}

```
### Try it
- [Demo of Class](https://jsfiddle.net/gh/get/library/pure/ibsheet/ibsheet8-manual-sample/tree/master/samples/properties/Col/Class/)
- [Demo of ClassFormula](https://jsfiddle.net/gh/get/library/pure/ibsheet/ibsheet8-manual-sample/tree/master/samples/properties/Col/ClassFormula/)


### Read More
- [setAttribute method](/docs/funcs/core/set-attribute)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
