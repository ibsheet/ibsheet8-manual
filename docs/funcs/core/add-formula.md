# addFormula ***(method)***

<!-- synonyms: 포뮬러 추가, 동적 Formula, addFormula, 수식 동적 적용, attribute+Formula 동적 추가 -->

> 특정 행·열·셀에 포뮬러를 동적으로 추가합니다.  
> 이 함수 사용 시 [CanFormula](/docs/props/row/can-formula)가 자동으로 `true`로 설정되고, [CalcOrder](/docs/props/row/calc-order)에도 추가한 포뮬러가 자동으로 등록됩니다.  
> `row`와 `col`이 생략되면 전체 데이터에 적용됩니다. 자세한 내용은 [Formula col](/docs/props/col/formula)을 참고하세요.
<!--!
> `[비공개 설명]` [CalcOrder](/docs/props/row/calc-order)가 def에 설정되어 있으면 def에, 로우 객체에 설정되어 있으면 로우객체에 추가됩니다.
!-->

### Syntax
```javascript
boolean addFormula( formula, row, col, attr, render );
```

### Parameters
|Name|Type|Required| Description |
|----------|-----|---|----|
|formula|`function` \| `string`|<span class='required'>필수</span>|추가하고자 하는 포뮬러|
|row |`object` \| `array[object]`|<span class='optional'>선택</span>|[데이터 로우 객체](/docs/appx/row-object) 또는 [데이터 로우 객체](/docs/appx/row-object) 배열|
|col |`string`|<span class='optional'>선택</span>|열 이름|
|attr|`string`|<span class='optional'>선택</span>|추가하려는 [attribute + Formula](/docs/props/col/attribute-formula)의 속성명|
|render|`boolean`|<span class='optional'>선택</span>|즉시 화면 반영 여부<br/>해당 기능을 `0(false)`로 사용했을 경우, 작업 마무리 시에 `rerender()`를 실행해야 화면에 반영 됩니다.<br/>`0(false)`:반영 안함<br/>`1(true)`:즉시 반영 (`default`)|

### Return Value
***boolean*** : 함수 정상 동작 여부. (인자값이 잘못되어 수행되지 못한 경우에는 false 리턴)

### Example
```javascript
// 컬럼 동적 추가 후 attribute+Formula로 배경색 적용 (attr="Color")
sheet.addCol("IntData", 0, -1, {Type:"Int", Header:"추가Int컬럼", Width:200, CanEdit:1}, true);

var colorFormula = function(param) {
    if (param.Row && param.Row["IntData"] === 0) {
        return "#FFD9FA";
    }
};
sheet.addFormula(colorFormula, "", "", "Color");


// 다른 컬럼 값에 따라 체크박스 자동 체크 (function 형식)
var Formula = function(param) {
    return param.Row["IntData"] > 100;
};
sheet.addFormula(Formula, "", "CheckData", "", true);


// 다른 컬럼 합산을 string 형식으로 특정 셀에만 적용
sheet.addFormula("IntData + FloatData", sheet.getFirstRow(), "TextData", "", true);
```

### Read More
- [Formula col](/docs/props/col/formula)
- [attribute+Formula col](/docs/props/col/attribute-formula)
- [attribute+Formula row](/docs/props/row/attribute-formula)
- [CanFormula row](/docs/props/row/can-formula)
- [CalcOrder row](/docs/props/row/calc-order)
- [FormulaRow col](/docs/props/col/formula-row)
- [calculate method](/docs/funcs/core/calculate)

### Since

|product|version|desc|
|---|---|---|
|core|8.2.0.4|기능 추가|
