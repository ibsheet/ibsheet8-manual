# FocusRow ***(cell)***

<!-- synonyms: FocusRow, focus-row, 포커스 행, 행 포커스, 커서 행, 커서 포커스 행, focus row, focused row, 행 하이라이트, 포커스 행 디자인, 포커스 행 스타일 -->

> 셀을 클릭시 보여지는 "커서 포커스 행"은 Table 객체 위에 DIV 객체가 떠있는 형태로 구성됩니다.
>
> 특정 셀에 포커스가 있을때 보여질 "커서 포커스 행"의 디자인을 설정합니다.
>
> 예약된 문자를 구분자 ","연결하여 설정합니다.
>
> 기본적으로는 "Border, Background"로 구성됩니다.

###
![FocusRow](/assets/imgs/focusRow1.png "FocusRow default")<br/>
[일반 FocusRow]

![FocusRow](/assets/imgs/focusRow2.png "FocusRow default")<br/>
[border없이 Background로 설정시]



### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`Border`|커서 포커스 DIV의 테두리 사용 (.IBFocusRowBorder)|
|`Background`|커서 포커스 DIV의 배경색 사용 (.IBFocusRowBackground) |
|`Color`|커서 포커스 DIV를 사용하지 않고 Table 객체에 background-color를 부여 (성능이 저하될수 있음,포커스 셀은 제외) (.IBColorFocused) |
|`Class`|css/default(테마)/main.css 파일에 .IBClassFocused 클레스에 정의한 디자인을 따릅니다. (포커스 셀은 제외)|

### Example
```javascript
//셀에 포커스가 들어갔을때 포커스행에 대해 배경색만 사용함
sheet.setAttribute(sheet.getRowById("AR99"), "CLS", "FocusRow", "Background");
```

### Read More
- [FocusRow row](/docs/props/row/focus-row)
- [FocusRow col](/docs/props/col/focus-row)
<!--!
- `[비공개]` [FocusCell row](/docs/props/row/focus-cell)
!-->
- [FocusCell col](/docs/props/col/focus-cell)
- [FocusCell cell](./focus-cell)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
