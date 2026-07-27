# setFormulaRow ***(method)***
> `FormulaRow`(합계행)에 계산을 변경(`Sum,Avg,Min,Max`)하거나 행을 감출 수 있습니다.  
> 컬럼에 `FormulaRow` 설정이 없어도 이 함수를 호출하면 동적으로 합계행이 생성됩니다.

### Syntax
```javascript
void setFormulaRow( val, cols, visible, render );
```

### Parameters


|Name|Type|Required| Description |
|----------|-----|---|----|
|val |`string` \| `object`|<span class='required'>필수</span>|설정할 계산 방식 (`'Sum'`,`'Avg'`,`'Min'`,`'Max'` 중 하나) <br/>또는 object 형태로 설정시 `{"ColName1":"Sum","ColName2":"Avg"}` 식으로 설정 가능<br/>(object형을 사용시에는 `cols` 인자는 필요 없음)|
|cols |`string`|<span class='optional'>선택</span>|계산할 열이름(복수개인 경우 ,를 구분자로 연결한 문자열)|
|visible |`boolean`|<span class='optional'>선택</span>|`FormulaRow` 보임 여부<br>`0(false)`:`FormulaRow`(합계행) 감춤 (`default`)<br>`1(true)`:`FormulaRow`(합계행) 보임|
|render |`boolean`|<span class='optional'>선택</span>|즉시 화면 반영 여부<br/>해당 기능을 `0(false)`로 사용했을 경우, 작업 마무리 시에 `rerender()`를 실행해야 화면에 반영 됩니다.<br/>`0(false)`:반영 안함 (`default`)<br/>`1(true)`:즉시 반영|

### Return Value
***boolean*** : 설정 완료 여부

### Example
```javascript
//합계행에 계산을 평균값으로 변경
sheet.setFormulaRow( "Avg", "AMT1,AMT2", 1, 1 );

//합계행을 감춘다.
sheet.setFormulaRow({visible:0, render:1});
```

### Read More
- [FormulaRow col](/docs/props/col/formula-row)
- [setFormulaRowPosition method](./set-formula-row-position)
- [NoCalculate row](/docs/props/row/no-calculate)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
