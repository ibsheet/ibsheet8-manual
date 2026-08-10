# NoColor ***(row)***

<!-- synonyms: no color, ignore background color, disable color, no background, transparent bg override, state color override, 배경색 무시, 배경색 없음, 색상 무시, 색상 제거, 상태 색상 무시, NoColor 속성 -->

> 행의 기본 적용된 배경색이 무시됩니다.  
> 홀수, 짝수행에 대한 배경색상([AlternateColor](./alternate-color))나 상태(입력, 수정, 삭제) 및 선택에 대한 색상이 무시되고, `Color` 속성을 통한 배경색도 적용되지 않게 할 수 있습니다.  
> [FormulaRow](/docs/props/col/formula-row)에 `NoColor`를 설정하여 해당 행의 배경색을 무시할 수 있습니다.  
> `NoColor`가 적용되는 우선 순위는 셀 \> 열 \> 행입니다.

### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`0`|기능 사용 안함(`default`)|
|`1`|모든 배경색 무시(단 Class속성을 통해 설정한 배경색을 적용)|
|`2`|상태 및 선택에 대한 색상만 무시|
|`3`|`Color` 설정 시 상태, `AlternateColor`에 대한 색상을 무시하고 `Color` 색상 적용|

### Example
```javascript
//특정행의 배경색 변경을 막는다.
var row = sheet.getRowById("AR11")
row["NoColor"] = 1;
sheet.refreshRow(row);

//데이터 행에 대해서 상태에 따른 배경색 변경 기능을 제한한다.
options.Def.Row = {"NoColor":2};
```
### Read More
- [ColorState cfg](/docs/props/cfg/color-state)
- [Alternate cfg](/docs/props/cfg/alternate)
- [Color row](./color)
- [AlternateColor row](./alternate-color)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.2.0.14|`NoColor: 3` 동작 추가|