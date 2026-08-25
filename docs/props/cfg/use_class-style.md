# UseClassStyle ***(cfg)***

<!-- synonyms: UseClassStyle, use class style, class css width height, css width height apply, class style, class 속성 사용, class CSS 크기, class 너비 높이, class CSS 시트 크기, css class 활용, 클래스 스타일 적용 -->

> 시트를 생성할 `div`(el)에 class가 지정되어 있으면, 그 class의 CSS에서 height와 width 값을 읽어 시트 생성 시 너비와 높이에 적용합니다.  
> class로 준 크기는 **`class` 속성에 지정한 class에서만** 읽습니다.  
> id 선택자(`#id{}`), 하위 선택자(`.wrap div{}`), 속성 선택자(`[data-x]{}`)처럼 class 속성이 아닌 방식으로 준 크기는 무시됩니다.  
> 너비와 높이는 인라인 `style`이 있으면 그 값을, 없으면 class 값을, 둘 다 없으면 기본값을 사용합니다.  
> <mark>*너비는 **100%**, 높이는 **800px**를 기본값으로 갖습니다.*</mark>  
> **<mark>주의</mark> : 시트 크기는 하나의 class로 지정하세요.** width와 height를 여러 class에 나눠 주면 의도대로 적용되지 않을 수 있습니다.


### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|기능 사용 안함 (`default`)|
|`1(true)`|시트 div에 선언된 class 정보를 확인하여, 시트의 너비와 높이에 적용|


### Example
```html
<!-- 시트 크기를 인라인 style이 아니라 class로 지정 -->
<style>
  .gridBox { width: 100%; height: 300px; }
</style>
<div id="sheetDiv" class="gridBox"></div>
```
```javascript
options.Cfg = {
    UseClassStyle: true   // div의 class(.gridBox)에 지정한 width/height를 시트 크기로 사용
};
IBSheet.create({ id: "sheet", el: "sheetDiv", options: options });
```

### Try it
- [Demo of UseClassStyle](https://jsfiddle.net/gh/get/library/pure/ibsheet/ibsheet8-manual-sample/tree/master/samples/properties/Cfg/UseClassStyle/)

### Read More
- [create static](/docs/static/create)
- [Quick Start getting started](/docs/start/quick-start)
- [시트객체 높이 설정 appendix](/docs/appx/sheet-height)

### Since

|product|version|desc|
|---|---|---|
|core|8.3.0.37|기능 추가|
