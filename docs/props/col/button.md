# Button ***(col)***

<!-- synonyms: 우측 버튼, 우측 체크박스, 우측 아이콘, 셀 우측 버튼, button column, popup 버튼 -->

> 셀 값의 우측에 원하는 아이콘 이미지, 체크박스 혹은 버튼을 표시하는 기능입니다.  
> `Date` 타입은 기본으로 셀 우측에 달력 버튼이 표시됩니다.  
> 셀의 좌측에 버튼을 설정하려면 [Icon](./icon) 속성을 참고하세요.

![Button: Clear — 셀 내용 지우기](/assets/imgs/button1.png "Button: Clear") [그림1]  
![Button: Check — 체크박스](/assets/imgs/button2.png "Button: Check") [그림2]  
![Button: URL — 사용자 이미지](/assets/imgs/button3.png "Button: URL 이미지") [그림3]  
![Button: Defaults — 드롭다운 버튼](/assets/imgs/buttonDefaults.png "Button: Defaults") [그림4]

### Type
`string`

### Options

**열의 Type이 Button이 아닌 경우**

|Value|Description|
|-----|-----|
|`Button`|[ButtonText](./button-text) 속성으로 설정한 문자를 `<u>` 태그로 표시합니다.|
|`Clear`|셀 우측에 셀 내용을 지우기 위한 버튼을 표시합니다 ([그림1] 참고).|
|`Check`|셀 우측에 체크박스를 표시합니다 ([그림2] 참고).|
|`Html`|[ButtonText](./button-text) 속성으로 지정한 HTML 태그를 셀 우측에 표시합니다.|
|`공백`|기본 버튼 이미지를 감춥니다. 예: `Date` 타입 열의 기본 달력 버튼을 이 속성으로 감출 수 있습니다.|
|`기타`|이미지 파일 URL을 지정하면 버튼 셀의 배경 이미지로 표시됩니다 ([그림3] 참고). 지원 포맷: `gif`, `png`, `jpg`. 클릭 시 [onButtonClick](/docs/events/on-button-click) 이벤트가 호출됩니다.|
|`Defaults`|셀 우측에 [Defaults](./defaults) 버튼을 표시합니다 ([그림4] 참고).|
<!--!
|`[비공개]` `Expand`|접음/펼침 기능을 사용하기 위한 버튼이 표시됩니다.|
!-->

> **주의**: `Button` 속성에는 위 표의 정해진 키워드(`Button` / `Clear` / `Check` / `Html` / `Defaults` / 공백) 또는 이미지 파일 URL만 지정해야 합니다.  
> 그 외의 문자열(예: `<u>...</u>` 같은 HTML 마크업)을 지정하면 해당 문자열을 이미지 URL로 간주하여, 그 경로로 불필요한 요청(대개 404)이 렌더마다 발생합니다.  
> 조건에 따라 HTML을 표시하려면 마크업을 `Button` 속성이 아니라 [ButtonText](./button-text)에 넣으세요.

> `Html`이나 이미지 버튼 사용 시 버튼 너비는 [WidthPad](./width-pad) 속성으로 설정할 수 있습니다.


**열의 Type이 Button인 경우**

|Value|Description|
|---|---|
|`Button`|일반적인 버튼 형태로 표시합니다. [UseButton](/docs/props/cfg/use-button) 속성에 따라 [ButtonText](./button-text)에 설정한 값이 `<u>` 태그 또는 `<button>` 태그로 렌더링됩니다.|
|`Html`|[ButtonText](./button-text)에 설정한 값을 HTML로 해석해 표시합니다 (예: `<div class="button">버튼</div>`).<br/>HTML 콘텐츠는 `ButtonText`에 넣으며, `Button` 속성 자체에는 HTML 마크업을 넣지 마세요.|
<!--!
|`[비공개]` `Class`|셀에 커스텀 css Class를 적용합니다.<br/>가령 기본테마를 사용하면서 `Button속성`의 값을 "Class"로, [ButtonClass](./button-class)속성의 값을 "CUST_BTN"으로 설정하면,<br/>실제 해당셀의 클레스는 **IBToolCUST_BTN** 으로 설정됩니다.| 
!-->

### Example
```javascript
options.Cols = [
    // 1. 셀 우측에 체크박스를 표시
    {Type: "Text", Name: "product_name", Button: "Check", Width: 120},

    // 2. 셀 우측에 사용자 이미지를 버튼으로 표시
    {Type: "Text", Name: "brnSaleAmt", Button: "/pcd/img/popIcon.png", Width: 120},

    // 3. Type:"Button" — 셀 자체가 버튼인 컬럼
    {Type: "Button", Name: "btn_type", Button: "Button", ButtonText: "Btn", Width: 120, WidthPad: 50}
];
```

### Try it
- [Demo of Button](https://portal.ibsheet.com/ko/support/solutions/articles/72000650961-셀-우측-버튼-button-속성-사용-방법)

### Read More
- [WidthPad col](./width-pad)
- [ButtonText col](./button-text)
- [Defaults col](./defaults)
- [UseButton cfg](/docs/props/cfg/use-button)
- [TreeCheckSync cfg](/docs/props/cfg/tree-check-sync)
- [Checked cell](/docs/props/cell/checked)
- [onButtonClick event](/docs/events/on-button-click)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
