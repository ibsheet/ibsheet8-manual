# AddClass ***(cell)***

<!-- synonyms: AddClass, add-class, 버튼 클래스 추가, CSS 클래스 추가, 버튼 스타일, 셀 버튼 CSS, 사용자 정의 클래스, button css class, add css class, custom class, button style -->

> 열의 Type이 `Button`이고 `Button` 속성의 값이 `Button`인 경우, 버튼 셀에 적용할 CSS Class 명을 설정합니다.

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
.MYBTN{color:#FF0000; font-weight:700;}
</style>
```
```javascript
//1. 함수를 이용하여 셀에 AddClass적용
sheet.setAttribute(sheet.getRowById("AR9"), "EDate", "AddClass", "MYBTN");


//2. 데이터 행객체(예: AR10)에 직접 접근하여 셀에 CSS 적용
var ROW = sheet.getRowById("AR10");
ROW["CLSAddClass"] = "MYBTN";
//변경내용 확인
sheet.refreshCell({row:ROW, col:"CLS"});


//3. 조회 데이터 내에서 속성설정(열이름이 CLS 로 가정)
{
    data:[
        {... , "CLSAddClass":"MYBTN" , ...}
    ]
}
```
### Try it
- [Demo of addClass](https://jsfiddle.net/gh/get/library/pure/ibsheet/ibsheet8-manual-sample/tree/master/samples/properties/Col/AddClassFormula/)

### Read More
- [Button col](/docs/props/col/button)
- [ButtonText col](/docs/props/col/button-text)
- [UseButton cfg](/docs/props/cfg/use-button)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
