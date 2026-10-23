# ShowHint ***(cell)***

<!-- synonyms: ShowHint, show-hint, 힌트 표시, 셀 힌트, 툴팁, 셀 미리보기, 감춰진 텍스트, 잘린 내용 힌트, 확장 표시, show hint, cell tooltip, cell hint, hover preview, tooltip, 힌트 끄기, 힌트 기능 끄기, 힌트 안 뜨게, 힌트 사용 안 함, 특정 셀 힌트 끄기, 셀별 힌트 설정, 말줄임 내용 보기, disable hint, hint off, 마우스 올리면 셀 커짐, 마우스 올리면 글자 튀어나옴, 마우스 오버 시 셀 늘어남, 셀 위에 박스가 뜸, 잘린 글자 팝업, 잘린 내용 전체 보기, 말줄임 전체 보기, 셀 내용 펼쳐 보기, 호버 시 전체 내용 표시, mouseover expand cell, truncated text popup -->

> 해당 셀에서 힌트 기능을 사용할지 여부를 설정합니다.  
> 힌트는 셀 내용이 잘려 보일 때, 마우스 커서가 올라간 셀을 일시적으로 늘려 가려진 내용을 보여주는 기능입니다.  
> 체크박스나 라디오 형태의 열에서는 작동하지 않으며, 셀에 설정한 값은 [ShowHint row](/docs/props/row/show-hint)와 [ShowHint col](/docs/props/col/show-hint) 설정보다 우선 적용됩니다.

###
![힌트활성화](/assets/imgs/hint1.png "마우스 커서가 셀에 올라갔을 때 힌트를 통해 감춰진 부분이 보여짐")<br/>


### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`0`|힌트 기능을 사용 안 함|
|`1`|셀의 크기가 작아 셀 내용의 일부만 보일 때 힌트 표시 (`default`)|
|`2`|`1`의 경우에 더해, 스크롤 때문에 셀 일부가 가려질 때도 힌트 표시|
|`3`|항상 힌트 표시. 힌트 내용은 [onShowHint](/docs/events/on-show-hint) 이벤트에서 변경 가능|


### Example
```javascript
//1. 메소드를 통해 특정 셀에 속성 적용 (열이름: CLS)
sheet.setAttribute(sheet.getRowById("AR99"), "CLS", "ShowHint", 0);

//2. 객체에 직접 접근해서 속성 적용 (열이름: CLS)
var ROW = sheet.getRowById("AR10");
ROW["CLSShowHint"] = 2;
//변경내용 확인
sheet.refreshCell(ROW, "CLS");

//3. 조회 데이터 내에서 속성 적용 (열이름: CLS)
{
    data:[
        {"CLS": "값", "CLSShowHint": 0}
    ]
}
```

### Read More
- [HintValue cell](./hint-value)
- [ShowHint row](/docs/props/row/show-hint)
- [ShowHint col](/docs/props/col/show-hint)
- [onShowHint event](/docs/events/on-show-hint)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
