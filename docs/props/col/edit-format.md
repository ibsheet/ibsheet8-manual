# EditFormat ***(col)***
> 셀을 편집 모드로 전환했을 때 적용되는 **입력 포맷(edit format)** 을 설정합니다.  
> `Format`이 화면에 표시되는 값을 정의한다면, `EditFormat`은 **사용자가 데이터를 편집할 때 표시되는 형식**을 정의합니다.  
> `EditFormat`은 열의 [Type](/docs/appx/type)에 따라 설정 방식과 동작이 달라지며, **`Date`, `Text`, `Lines` 타입에서 사용할 수 있습니다.**  
>
> **자세한 포맷 규칙은 appendix의 [Format](/docs/appx/format)을 참고해 주세요.**


### Type
`mixed` ( `string` \| `object`)

### Options
|Column Type|Type|Description|
|---|---|---|
|`Text, Lines`|`object`|편집 모드에서 표시할 값 매핑을 정의합니다.<br/>ex) 셀의 값이 `USA`인 경우 편집 모드에서 `미국`으로 표시됩니다.<br/><br/>"EditFormat":{"KOR":"대한민국", "JPN":"일본", "USA":"미국"}<br/>![EditFormat Text](/assets/imgs/editFormatText.png)|
|`Date`|`string`|편집 모드에서 입력 및 표시될 날짜 형식을 지정합니다.<br/>ex)"EditFormat":"ddMMyyyy"<br/>![EditFormat Date](/assets/imgs/editFormatDate.png)|


### Example
```javascript
// 특정 열에서 편집 시 날짜를 일-월-년 순서로 표시
options.Cols = [
    {
        Type: "Date", 
        Format: "yyyy-MM-dd", //보여지는 포맷
        EditFormat: "ddMMyyyy", //편집시 포맷
        Name: "enterDate",
        Width: 120
    }

];
```

### Read More
- [Format col](./format)
- [DataFormat col](./data-format)
- [EditFormat cell](/docs/props/cell/edit-format)
- [Format appendix](/docs/appx/format)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
