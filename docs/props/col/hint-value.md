# HintValue ***(col)***

<!-- synonyms: 힌트 값, 툴팁 값, 셀 힌트, 힌트 텍스트, 잘린 값 표시, hint value, cell hint, tooltip value, hover value -->

> 해당 열에서 힌트가 표시될 때, 셀 내용 대신 보여줄 문자를 설정합니다.  
> 셀 내용이 잘리지 않은 셀에는 힌트가 표시되지 않으므로, 잘리지 않은 셀에도 표시하려면 [ShowHint](/docs/props/col/show-hint)를 `3`으로 설정합니다.  
> [HintValue row](/docs/props/row/hint-value)나 [HintValue cell](/docs/props/cell/hint-value)이 설정된 행이나 셀에는 그 설정이 우선 적용됩니다.

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
options.Cols = [
    // 내용이 잘린 셀에 마우스를 올리면 "이번 분기는 마감되었습니다." 표시
    {Type: "Text", Name: "DESC", Width: 120, HintValue: "이번 분기는 마감되었습니다."},
    // 내용이 잘리지 않은 셀에도 "마감" 표시
    {Type: "Text", Name: "STATUS", Width: 80, HintValue: "마감", ShowHint: 3}
];
```

### Read More
- [HintValue row](/docs/props/row/hint-value)
- [HintValue cell](/docs/props/cell/hint-value)
- [ShowHint col](./show-hint)
- [ShowHint row](/docs/props/row/show-hint)
- [onShowHint event](/docs/events/on-show-hint)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
