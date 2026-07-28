# Class ***(row)***

> 행에 포함된 각 셀에 `사용자 정의 CSS`를 설정합니다.

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
/* 텍스트를 깜빡이게 설정 */
.rowAlert {font-weight:700; animation:blinkingText 1s infinite;}
@keyframes blinkingText{
0%{     color: #FF0000;    }
50%{     color: #FF0000;    }
80%{    color:transparent;  }
100%{   color: #FF0000;    }
}

/* 텍스트의 색상과 배경색 설정 */
.subTitle{color:#EDEDED; background-color:#666666;}
</style>
```
```javascript

//1. 데이터 행객체(예: AR11)에 직접 접근하여 CSS 적용
var row = sheet.getRowById("AR11")
row["Class"] = "rowAlert";
sheet.refreshRow(row);

//2. 함수를 이용하여 CSS 적용
var row = sheet.getRowById("AR1");
sheet.setAttribute({ "row" :row ,"attr":"Class", "val":"rowAlert" });

// 헤더 행에 CSS 적용
options = {
    Cfg : {...},
    Def : {
        Header : {
            // 헤더행의 Text와 배경 색상을 변경한다.
            "Class": "subTitle"
        }
    },
    Cols : [
       {Header: "상세정보", Type: "Text", Name: "Detail"}
    ]
}

```
### Try it
- [Demo of Class](https://jsfiddle.net/gh/get/library/pure/ibsheet/ibsheet8-manual-sample/tree/master/samples/properties/Row/Class/)
- [Demo of ClassFormula](https://jsfiddle.net/gh/get/library/pure/ibsheet/ibsheet8-manual-sample/tree/master/samples/properties/Row/ClassFormula/)

### Read More
- [setAttribute method](/docs/funcs/core/set-attribute)
- [AlternateClass row](./alternate-class)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
