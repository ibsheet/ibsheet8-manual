# EditFormat ***(cell)***

> 셀을 편집 모드로 전환했을 때 적용되는 **입력 포맷(edit format)** 을 설정합니다.  
> `Format`이 화면에 표시되는 값을 정의한다면, `EditFormat`은 **사용자가 데이터를 편집할 때 표시되는 형식**을 정의합니다.  
> `EditFormat`은 셀의 [Type](/docs/appx/type)에 따라 설정 방식과 동작이 달라지며, **`Date`, `Text`, `Lines` 타입에서 사용할 수 있습니다.**  
>
> **자세한 포맷 규칙은 appendix의 [Format](/docs/appx/format)을 참고해 주세요.**


### Type
`mixed`( `string` \| `object` )

### Options
| Column Type | Type | Description |
|---|---|---|
|`Text, Lines`|`object`|편집 모드에서 표시할 값 매핑을 정의합니다.<br/>ex) 셀의 값이 `USA`인 경우 편집 모드에서 `미국`으로 표시됩니다.<br/><br/>"EditFormat":{"KOR":"대한민국", "JPN":"일본", "USA":"미국"}<br/>![EditFormat Text](/assets/imgs/editFormatText.png)|
|`Date`|`string`|편집 모드에서 표시될 날짜 형식을 지정합니다.<br/>ex)"EditFormat":"ddMMyyyy"<br/>![EditFormat Date](/assets/imgs/editFormatDate.png)|


### Example
```javascript
//1. 메소드를 통해 특정 셀의 EditFormat 변경
sheet.setAttribute( sheet.getRowById("AR9") , "EDate" , "EditFormat" ,"MMddyyyy");


//2. 객체에 직접 접근하여 EditFormat 변경
var ROW = sheet.getRowById("AR10");
ROW["EDateEditFormat"] = "ddMMyyyy";

//변경내용 반영
sheet.refreshCell({row:ROW, col:"EDate"});


//3. 조회 데이터 내에서 EditFormat 변경
{
    data:[
        { "EDateEditFormat":"yyyyMMdd" }
    ]
}
```

### Read More
- [Format cell](./format)
- [DataFormat cell](./data-format)
- [EditFormat col](/docs/props/col/edit-format)
- [Format appendix](/docs/appx/format)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
