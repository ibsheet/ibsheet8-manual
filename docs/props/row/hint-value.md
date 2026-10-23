# HintValue ***(row)***

<!-- synonyms: hint value, row hint text, hint content, tooltip value, overflow hint, hover hint, 힌트 값, 힌트 내용, 힌트 텍스트, 마우스 오버 안내, 셀 힌트, 감춘 내용 표시, HintValue 속성 -->

> 해당 행에서 힌트가 표시될 때, 셀 내용 대신 보여줄 문자를 설정합니다.  
> 셀 내용이 잘리지 않은 셀에는 힌트가 표시되지 않으므로, 잘리지 않은 셀에도 표시하려면 [ShowHint](/docs/props/row/show-hint)를 `3`으로 설정합니다.  
> 행에 설정한 값은 [HintValue col](/docs/props/col/hint-value) 설정보다 우선 적용되고, [HintValue cell](/docs/props/cell/hint-value)이 설정된 셀에는 셀 설정이 적용됩니다.

###
![HintValue](/assets/imgs/hintValue.png "마우스 커서가 셀에 오버 시 설정한 글자가 보여짐")

### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`string`|힌트가 표시될 때 셀 내용 대신 보여줄 문자|

### Example
```javascript
//10번 행에 대해서는 힌트 기능 사용 시 원래 내용과 다른 내용이 보여지게끔 한다.
var row = sheet.getRowById("AR10");
row["HintValue"] = "해당 건은 결제가 완료되었습니다.";

//조회 데이터에서 일부 행에 대해 원래 셀의 내용과 다른 내용이 보여지게끔 한다.
{"data":[
    {"HintValue": "의심거래항목입니다.", "ColName1": "Value1", "ColName2": "Value2"},
    {"ColName1": "Value3", "ColName2": "Value4"}
]}
```

### Read More
- [HintValue col](/docs/props/col/hint-value)
- [HintValue cell](/docs/props/cell/hint-value)
- [ShowHint row](./show-hint)
- [onShowHint event](/docs/events/on-show-hint)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
