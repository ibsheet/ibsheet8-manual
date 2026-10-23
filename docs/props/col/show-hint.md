# ShowHint ***(col)***

<!-- synonyms: 힌트 표시, 툴팁 표시, 잘린 셀 표시, 마우스 힌트, show hint, tooltip show, hover hint, cell hint show, 힌트 끄기, 힌트 기능 끄기, 힌트 안 뜨게, 힌트 사용 안 함, 시트 전체 힌트 끄기, 열 힌트 끄기, 말줄임 내용 보기, Def.Col ShowHint, disable hint, hint off, 마우스 올리면 셀 커짐, 마우스 올리면 글자 튀어나옴, 마우스 오버 시 셀 늘어남, 셀 위에 박스가 뜸, 잘린 글자 팝업, 잘린 내용 전체 보기, 말줄임 전체 보기, 셀 내용 펼쳐 보기, 호버 시 전체 내용 표시, mouseover expand cell, truncated text popup -->

> 해당 열에서 힌트 기능을 사용할지 여부를 설정합니다.  
> 힌트는 셀 내용이 잘려 보일 때, 마우스 커서가 올라간 셀을 일시적으로 늘려 가려진 내용을 보여주는 기능입니다.  
> 체크박스나 라디오 형태의 열에서는 작동하지 않으며, [ShowHint row](/docs/props/row/show-hint)나 [ShowHint cell](/docs/props/cell/show-hint)이 설정된 행이나 셀에는 그 설정이 우선 적용됩니다.

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
// 예 1) 특정 열에 ShowHint 설정
options.Cols = [
    // 셀 내용이 잘리거나, 스크롤 때문에 셀 아랫부분이 가려질 때 힌트 표시
    {Type: "Text", Name: "DESC", Width: 120, ShowHint: 2}
];

// 예 2) 모든 열의 힌트를 끄고, DESC 열만 힌트 표시
options.Def = {
    Col: {ShowHint: 0}
};
options.Cols = [
    {Type: "Text", Name: "CODE", Width: 80},
    {Type: "Text", Name: "DESC", Width: 120, ShowHint: 1}
];
```

### Read More
- [HintValue col](./hint-value)
- [ShowHint row](/docs/props/row/show-hint)
- [ShowHint cell](/docs/props/cell/show-hint)
- [onShowHint event](/docs/events/on-show-hint)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
