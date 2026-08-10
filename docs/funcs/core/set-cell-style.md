# setCellStyle ***(method)***

<!-- synonyms: setCellStyle, set-cell-style, 셀 스타일, 셀 스타일 설정, 스타일 변경, style 속성, 셀 서식, 스타일 적용, style, set style, cell style, apply style, change style -->

> 특정 셀의 style속성 값을 변경합니다.
>
> `row`를 `null`로 설정시 열에 대한 속성으로 설정됩니다.
>
> `col`을 `null`로 설정시 행에 대한 속성으로 설정됩니다.
### Syntax
```javascript
void setCellStyle( row, col, styleAttr, render );
```

### Parameters

|Name|Type|Required| Description |
|----------|-----|---|----|
|row |`object`|<span class='optional'>선택</span>|[데이터 로우 객체](/docs/appx/row-object)|
|col |`string`|<span class='optional'>선택</span>|열이름|
|styleAttr|`object`|<span class='required'>필수</span>|확인하고 싶은 style 속성값<br/>`'Color'(배경색)`, `'TextColor'(텍스트의 컬러)`, `'TextSize'(텍스트 크기)`, `'TextStyle'(텍스트의 스타일)`, `'TextFamily'(텍스트 폰트)`, `'Align'(정렬)` |
|render|`boolean`|<span class='optional'>선택</span>|즉시 화면 반영 여부<br/>해당 기능을 `0(false)`로 사용했을 경우, 작업 마무리 시에 `rerender()`를 실행해야 화면에 반영 됩니다.<br/>`0(false)`:반영 안함 (`default`)<br/>`1(true)`:즉시 반영|
### Return Value
***none***

### Example
```javascript
//셀의 글자색을 변경한다.
sheet.setCellStyle( sheet.getFirstRow(), "CUST_CD", {"TextColor" : "#FF0000"}, 1);

//행의 글자크기를 변경한다
sheet.setCellStyle( sheet.getRowByIndex(4), null, {"TextSize": 20 }, 1 );

```

### Read More
- [setAttribute method](./set-attribute)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
