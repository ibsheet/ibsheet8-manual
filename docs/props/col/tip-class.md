# TipClass ***(col)***

> 풍선도움말 객체에 원하는 `css클래스`를 적용하여 디자인을 설정 합니다.
>
> [Tip](./tip) 기능이 활성화된 경우에만 적용됩니다. 


### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`string`|풍선도움말 객체에 적용할 클래스 명|

### Example
```css
<style>
    .RedBold{color:red;font-weight:700;}
    .deepblue{color:#020079;}
</style>
```
```javascript

//1. 함수를 이용하여 CSS 적용
sheet.setAttribute({ "col" :"procs" ,"attr":"TipClass", "val":"RedBold" });

//2. 특정 열에 풍선도움말 표시시 사용될 클레스를 설정.
options.Cols = [
    ...
    {Type:"Text", Tip: 1, TipClass: "deepblue", Name: "procs", Width: 120 ...},
    ...
];
```

### Read More
- [Tip col](./tip)
- [Tip+Value col](./tip-value)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
