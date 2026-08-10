# AlternateClass ***(row)***

<!-- synonyms: alternate class, zebra stripe class, even row class, odd row class, striped rows css, alternate row css, 짝수행 클래스, 홀수행 클래스, 얼룩말 무늬 CSS, 교차 색상 클래스, 짝수행 CSS, AlternateClass 속성 -->

> 가독성을 높이기 위해서 홀수행, 짝수행 행의 배경색상을 다르게 설정할 때, 짝수행에 적용될 `css 클래스명`을 설정합니다.
>
> 이 속성은 [Alternate](/docs/props/cfg/alternate)에 영향을 받습니다.

### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`string`|css 클래스 명|

### Example
```css
<style>
    .alternateRow{background-color:#EDEDED;color:#666666;}
</style>
```
```javascript
//데이터 영역의 짝수행의 클래스를 지정한다.
options.Def.Row = {"AlternateClass": "alternateRow"};
```

### Read More
- [Alternate cfg](/docs/props/cfg/alternate)
- [AlternateColor row](/docs/props/row/alternate-color)
- [AlternateCount cfg](../cfg/alternate-count)
- [AlternateStart cfg](../cfg/alternate-start)
- [AlternateType cfg](../cfg/alternate-type)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
