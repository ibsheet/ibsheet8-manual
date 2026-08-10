# setAttribute ***(method)***

<!-- synonyms: setAttribute, set-attribute, 속성 설정, 속성 지정, 셀 속성 설정, 행 속성 설정, 열 속성 설정, set, attribute, property, assign -->

> 특정 `행(Row)`, `열(Col)`, `셀(Cell)`에 속성을 설정합니다.  
> `row`를 `null`로 설정시 `열`에 대한 속성으로 설정됩니다.  
> `col`을 `null`로 설정시 `행`에 대한 속성으로 설정됩니다.  
> 모든 속성을 설정할 수 있는 것은 아니기 때문에 해당 속성에 대해 설정하는 함수가 있다면 그 함수를 사용하실 것을 권합니다.  
> 예를 들어 행이나 컬럼을 숨기는 `Visible` 속성은 setAttribute 대신 전용 함수를 사용하세요.  
> - [hideCol](/docs/funcs/core/hide-col), [showCol](/docs/funcs/core/show-col), [hideRow](/docs/funcs/core/hide-row)

### Syntax
```javascript
void setAttribute( row, col, attr, val, render );
```

### Parameters
|Name|Type|Required| Description |
|----------|-----|---|----|
|row |`object`|<span class='optional'>선택</span>|[데이터 로우 객체](/docs/appx/row-object)|
|col |`string`|<span class='optional'>선택</span>|열이름|
|attr|`string`|<span class='required'>필수</span>|설정하고자 하는 속성명|
|val|`mixed`|<span class='required'>필수</span>|설정하고자 하는 속성 값|
|render|`boolean`|<span class='optional'>선택</span>|즉시 화면 반영 여부<br/>해당 기능을 `0(false)`로 사용했을 경우, 작업 마무리 시에 `rerender()`를 실행해야 화면에 반영 됩니다.<br/>`0(false)`:반영 안함<br/>`1(true)`:즉시 반영 (`default`)|

### Return Value
***none***

### Example
```javascript
//현재 포커스된 셀의 배경색을 붉은색으로 변경
sheet.setAttribute(sheet.getFocusedRow(), sheet.getFocusedCol() ,"Color" ,"#FF0000" ,1);

//특정 열에 편집을 불가능하게 변경
sheet.setAttribute(null, "ColName", "CanEdit", 0, 1);

//특정 행의 글자를 두껍게 변경 (col 생략 시 행 단위 설정)
sheet.setAttribute({row:sheet.getRowById("AR20"), attr:"TextStyle", val:1, render:1});

// 특정 값 셀 색상 강조
// setAttribute 호출 시마다 렌더링을 막고, 반복 처리 완료 후 rerender로 일괄 반영하여 성능 개선
var rows = sheet.getDataRows();

for (var r = 0; r < rows.length; r++) {
    var row = rows[r];

    if (row["TextData"] === "정상호") {
        sheet.setAttribute(
            row,       
            "TextData",
            "Color",
            "#FF0000",
            0
        );
    }
}

//일괄 반영
sheet.rerender(1);

```

### Read More
- [getAttribute method](./get-attribute)
- [setValue method](./set-value)
- [rerender method](./rerender)
- [refreshCell method](./refresh-cell)
- [refreshRow method](./refresh-row)
- [refreshPage method](./refresh-page)
- [renderBody method](./render-body)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
