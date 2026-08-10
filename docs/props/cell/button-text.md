# ButtonText ***(cell)***

<!-- synonyms: ButtonText, button-text, 버튼 문자열, 버튼 텍스트, 버튼 라벨, 버튼 표시 문자, 셀 버튼 텍스트, HTML 버튼 텍스트, button label, button caption, cell button text -->

> [Button](/docs/props/cell/button)속성의 값이 `Button`이거나 `Html`인 경우, 셀 버튼에 표시할 문자를 설정합니다.
>
> `Button속성`의 값이 `Button`인 경우에는 설정한 문자가 \<u>나 \<button>태그로 표시되며, <br/>`Html`인 경우에는 <span>입력</span>식의 Html 문자가 해석되어 셀에 표시됩니다.


### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`string`|버튼에 들어갈 문자열|

### Example
```javascript
//1. 메소드를 통해 특정 셀에 속성 적용 (열이름 :CLS)
sheet.setAttribute(sheet.getRowById("AR99"), "CLS", "ButtonText", "확인");


//2. 객체에 직접 접근해서 속성 적용 (열이름 :CLS)
var ROW = sheet.getRowById("AR10");
ROW["CLSButtonText"] = "<span class='spBtn'>완료</spn>";
//변경내용 확인
sheet.refreshCell({row:ROW, col:"CLS"});


//3. 조회 데이터 내에서 속성 적용  (열이름 :CLS)
{
    data:[
        {..., "CLSButtonText":"보류" , ...}
    ]
}
```

### Read More
- [Button cell](/docs/props/cell/button)
- [UseButton cfg](/docs/props/cfg/use-button)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
