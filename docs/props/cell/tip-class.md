# TipClass ***(cell)***

> 풍선도움말 객체에 원하는 `css클래스`를 적용하여 디자인을 설정 합니다.
>
> [Tip](./tip) 기능이 활성화된 경우에만 적용됩니다. 

### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`string`|풍선도움말 객체에 적용할 클레스 명|

### Example
```css
<style>
    .RedBold{color:red;font-weight:700;}
    .deepblue{color:#020079;}
</style>
```
```javascript

//1. 함수를 이용하여 CSS 적용
sheet.setAttribute(sheet.getRowById("AR10"), "CLS", "TipClass", "RedBold");

//2. 데이터 행객체(예: AR10)에 직접 접근하여 CSS 적용
var ROW = sheet.getRowById("AR10");
ROW["CLSTipClass"] = "deepblue";
//변경내용 확인
sheet.refreshCell({row:ROW, col:"CLS"});

//3. 조회 데이터 내에서 속성 적용 (열이름: CLS)
{
    data:[
        {... , "CLSTipClass": "RedBold", ...}
    ]
}
```

### Read More
- [Tip cell](./tip)
- [Tip+Value cell](./tip-value)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
