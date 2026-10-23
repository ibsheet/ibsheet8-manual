# HintValue ***(cell)***

<!-- synonyms: HintValue, hint-value, 힌트, 힌트 값, 툴팁, tooltip, hint value, hint text, 셀 힌트, 힌트 텍스트, 힌트 대체값, 마우스 오버 힌트 -->

> 해당 셀에서 힌트가 표시될 때, 셀 내용 대신 보여줄 문자를 설정합니다.  
> 셀 내용이 잘리지 않은 셀에는 힌트가 표시되지 않으므로, 잘리지 않은 셀에도 표시하려면 [ShowHint](/docs/props/cell/show-hint)를 `3`으로 설정합니다.  
> 셀에 설정한 값은 [HintValue row](/docs/props/row/hint-value)와 [HintValue col](/docs/props/col/hint-value) 설정보다 우선 적용됩니다.

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
//1. 메소드를 통해 특정 셀에 속성 적용 (열이름: CLS)
sheet.setAttribute(sheet.getRowById("AR99"), "CLS", "HintValue", "먼저 '실적대차' 열의 내용을 확인해 주세요.");

//2. 객체에 직접 접근해서 속성 적용 (열이름: CLS)
var ROW = sheet.getRowById("AR10");
ROW["CLSHintValue"] = "마감되었습니다.";
//변경내용 확인
sheet.refreshCell(ROW, "CLS");

//3. 조회 데이터 내에서 속성 적용 (열이름: CLS)
{
    data:[
        {"CLS": "값", "CLSHintValue": "공사 시작일을 먼저 입력해 주세요."}
    ]
}
```

### Read More
- [HintValue row](/docs/props/row/hint-value)
- [HintValue col](/docs/props/col/hint-value)
- [ShowHint cell](./show-hint)
- [ShowHint col](/docs/props/col/show-hint)
- [ShowHint row](/docs/props/row/show-hint)
- [onShowHint event](/docs/events/on-show-hint)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
