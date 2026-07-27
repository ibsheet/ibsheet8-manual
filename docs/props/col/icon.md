# Icon ***(col)***

<!-- synonyms: 좌측 아이콘, 좌측 체크박스, 좌측 버튼, 셀 좌측 아이콘, icon column, 체크박스 표시 -->

> 셀의 좌측에 원하는 아이콘 이미지, 체크박스 혹은 버튼을 표시하는 기능입니다.  
> 셀의 우측에 버튼을 표시하는 [Button](/docs/props/col/button) 속성과 유사한 기능입니다.  
> 열의 타입이 `Button`인 경우에는 사용하실 수 없습니다.

![Icon: Date — 달력 아이콘](/assets/imgs/Icon2.png "Icon: Date") [그림1]  
![Icon: URL — 사용자 이미지](/assets/imgs/Icon1.png "Icon: URL 이미지") [그림2]  
![Icon: Defaults — 드롭다운 버튼](/assets/imgs/iconDefaults.png "Icon: Defaults") [그림3]

### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`Clear`|셀 내용을 지우기 위한 버튼을 표시합니다.|
|`Date`|달력 아이콘을 표시합니다. 열의 타입이 `Date`인 경우 클릭 시 달력이 표시됩니다 ([그림1] 참고).|
|`Check`|체크박스를 표시합니다.|
|`공백`|원래 표시되어야 할 `Icon` 이미지를 감춥니다.|
|`기타`|이미지 파일 URL을 지정하면 아이콘 배경 이미지로 표시됩니다 ([그림2] 참고). 지원 포맷: `gif`, `png`, `jpg`.|
|`Defaults`|[Defaults](./defaults) 버튼을 표시합니다 ([그림3] 참고).|
<!--!
|`[비공개]` `Expand`|접음/펼침 기능을 사용하기 위한 버튼이 표시됩니다.|
!-->

> 아이콘 영역의 너비는 [IconWidth](/docs/props/col/icon-width) 속성으로 설정합니다.  
> 아이콘 클릭 시 [onIconClick](/docs/events/on-icon-click) 이벤트가 호출됩니다.  
> 단, `Clear`나 `Check`로 설정하면 [OnClickSide](/docs/props/event/on-click-side) 이벤트만 호출됩니다.

### Example

```javascript
options.Cols = [
    // 1. 셀 좌측에 체크박스를 표시
    {Type: "Text", Name: "product_name", Icon: "Check", Width: 120},

    // 2. 셀 좌측에 사용자 이미지를 아이콘으로 표시
    {Type: "Text", Name: "brnSaleAmt", Icon: "/pcd/img/popIcon.png", IconWidth: 15, Width: 120}
];

// 3. Icon:"Check" 사용 시 조회 데이터에서 체크 상태 지정 (열이름: product_name)
{
    "data": [
        { ..., "product_nameChecked": 1, ... }
    ]
}
```

### Try it
- [Demo of Icon](https://portal.ibsheet.com/ko/support/solutions/articles/72000650962-셀-좌측-버튼-icon-속성-사용-방법)

### Read More

- [IconWidth col](/docs/props/col/icon-width)
- [Button col](/docs/props/col/button)
- [Defaults col](./defaults)
- [Checked cell](/docs/props/cell/checked)
- [Icon cell](/docs/props/cell/icon)
- [IconWidth cell](/docs/props/cell/icon-width)
- [setIconCheck method](/docs/funcs/core/set-icon-check)
- [onIconClick event](/docs/events/on-icon-click)
- [TreeCheckSync cfg](/docs/props/cfg/tree-check-sync)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
