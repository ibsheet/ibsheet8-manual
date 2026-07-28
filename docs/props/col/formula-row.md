# FormulaRow ***(col)***

<!-- synonyms: 합계행, 합계, 평균, 최대값, 최소값, 건수, foot, 푸터, formula row -->

> `Foot` 영역에 고정된 행을 생성하여 열의 합계나 평균값을 보여줍니다.  
> `id`는 `FormulaRow`로 생성되며, `NoColor:2` 속성이 기본으로 들어갑니다.  
> `SearchMode:3, 4, 5`에서는 사용할 수 없습니다.  
> 숫자형 컬럼(`Int`, `Float`)을 제외한 다른 컬럼은 `"Count"`만 사용 가능합니다.

![FormulaRow](/assets/imgs/formulaRow.png)
![FormulaRow](/assets/imgs/formulaRow1.png)
### Type
`mixed`( `string` \| `function` )

### Options

|Value|Description|
|-----|-----|
|`'Sum'` 또는 `'합계 {Sum} 원'`|열의 합계값|
|`'Avg'` 또는 `'평균 {Avg}'`|열의 평균값|
|`'Max'` 또는 `'최대값 {Max}'`|열의 최대값|
|`'Min'` 또는 `'최소값 {Min}'`|열의 최소값|
|`'Count'` 또는 `'{Count} 건'`|행의 개수|
|`function`|사용자 정의 함수|

### Example

```javascript
options.Cols = [
    // ...
    {
        Type: "Int",
        Name: "qt",
        FormulaRow: "Sum",
        Width: 120,
        // ...
    },
    {
        Type: "Int",
        Name: "rate",
        FormulaRow: "Avg",
        Width: 120,
        // ...
    },
    {
        Type: "Int",
        Name: "brnSaleAmt",
        FormulaRow: "최대값 {Max}", //FormulaRow 행에 text+값 형태로 표현
        Width: 120,
        // ...
    },
    {
        //사용자 정의 함수(글자색이 "#FF0000"인 행의 수 리턴)
        Type: "Text",
        Name: "user",
        FormulaRow: function(fr){
            var rows = fr.Sheet.getDataRows();
            var count = 0;
            for(var i = 0; i < rows.length; i++){ //row의 TextColor 색상이 빨간색만 count
                if( rows[i].TextColor == "#FF0000"){
                    count++;
                }
            }
            return "경고 :" + count + "건";
        },
        Width: 120,
        // ...
    },
    // ...
];


// 객체 직접 접근하여 FormulaRow 행의 sDetail셀 값 교체
sheet.getRowById("FormulaRow")["sDetailVisible"] = 1; // 셀의 Visible 속성변경.
sheet.getRowById("FormulaRow")["sDetail"] = "가나다";
sheet.refreshRow(sheet.getRowById("FormulaRow"));

//setValue로 값 교체 (FormulaRow 속성이 없는 컬럼의 셀만 변경 가능)
//Sum/Avg 등 집계가 설정된 컬럼의 셀은 자동 계산되므로 setValue로 바꿀 수 없습니다.
sheet.setValue(sheet.getRowById("FormulaRow"),"sDetail","가나다");

```

### Read More
- [setFormulaRow method](/docs/funcs/core/set-formula-row)
- [setFormulaRowPosition method](/docs/funcs/core/set-formula-row-position)
- [NoCalculate row](/docs/props/row/no-calculate)
- [ExcludeEmpty col](/docs/props/col/exclude-empty)
- [NoColor row](/docs/props/row/no-color)

### Since
|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.2.0.3|{Sum, Avg, Max, Min, Count} 기능 추가|