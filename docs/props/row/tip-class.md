# TipClass ***(row)***

> 풍선도움말 객체에 원하는 `css클래스`를 적용하여 디자인을 설정 합니다.
>
> [Tip](./tip) 기능이 활성화된 경우에만 적용됩니다.  

### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`string`|풍선도움말 객체에 적용할 css클래스 명|

### Example
```css
<style>
    .RedBold{color:red;font-weight:700;}
    .deepblue{color:#020079;}
</style>
```
```javascript

//1. 함수를 이용하여 CSS 적용
var row = sheet.getRowById("AR1");
sheet.setAttribute({ "row" :row ,"attr":"TipClass", "val":"RedBold" });

//2. 데이터 행객체(예: AR11)에 직접 접근하여 CSS 적용
var row = sheet.getRowById("AR11");
row["TipClass"] = "RedBold";

//3. 조회 데이터에서 일부 행에 대해 풍선도움말 클레스를 설정.
{"data":[
    {"TipClass":"deepblue","ColName1":"Value1","ColName2":"Value2", ...},
    ...
]}
```

### Read More
- [Tip row](./tip)
- [TipPosition row](./tip-position)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
