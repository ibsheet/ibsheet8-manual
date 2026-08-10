# Visible ***(cell)***

<!-- synonyms: 보임, 감춤, 표시, 숨김, 셀 보임, 셀 숨김, 데이터 감춤, 데이터 표시, 값 숨기기, 값 감추기, visible, hide, hidden, display value -->

> 셀 데이터의 보임/감춤 여부를 설정합니다.
>
> 이 속성은 셀에 표시되는 데이터 값의 표시 여부만 제어합니다.
>
> 따라서 셀 타입(Button, Bool, Enum, File 등)에 따른 **UI 요소 및 사용자 인터랙션은 유지**됩니다.
>
> 예를 들어 Enum 타입은 List박스가 열리며, Bool 타입은 체크/해제 동작이 가능합니다.
>
> 셀의 편집 및 동작을 제한하려면 `CanEdit`, `Disabled`등의 속성을 사용해야 합니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|감춰짐|
|`1(true)`|보임(default)|

### Example
```javascript
// 첫번째행 "CLS" 컬럼에 해당하는 셀의 데이터를 감춘다.
sheet.setAttribute(sheet.getRowById("AR1"), "CLS", "Visible", 0, 1);


//조회 데이터에서 특정셀을 감춘다.
{"data":[
    ...
    {"ColName1Visible": 0, "ColName1": "Value1", "ColName2": "Value2", ...},
    ...
]}
```


### Read More
- [Visible row](/docs/props/row/visible)
- [Visible col](/docs/props/col/visible)
### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
