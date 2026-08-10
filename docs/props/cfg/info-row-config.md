# InfoRowConfig ***(cfg)***

<!-- synonyms: InfoRowConfig, info row config, information row, paging row, count row, status row, InfoRow, 정보 행, 건수 표시 행, 페이지 네비게이션, 페이징 표시, InfoRow 설정, Paging Count, StatusLabel, SummaryLabel -->

> 시트 상단 혹은 하단에 별도의 행을 통해 조회된 데이터의 개수나 페이지 네비게이션을 설정합니다.  
> 건수정보표시행에 임의의 문자나 숫자를 추가적으로 설정 하는 것도 가능합니다.  
> `Layout`에 셀에 대한 속성 및 타입을 설정 할 수 있습니다.  
> InfoRow 행의 높이는 이 옵션이 아니라 `Def.InfoRow.Height`로 지정합니다. (예: `Def: { InfoRow: { Height: 30 } }`)  
> InfoRow도 내부적으로 Formula를 지원하므로, `Layout` 셀에 `Formula` 함수를 지정해 계산 값을 표시할 수 있습니다.

### Type
`object`

### Options
|Value|Type|Description|
|----------|-----|---|
|Visible|`boolean`|정보 행을 화면에 표시할지 여부<br>`0(false)`:정보 행 화면에 표시 안함  (`SearchMode : 0,2,3 default`)<br>`1(true)`:정보 행 화면에 표시 (`SearchMode : 1,4,5 default`)|
|Layout|`array`\[`string`\|`object`\]|페이징, 건수 정보 표시, 선택 영역 합계/평균 표시, 상태 정보 표시, 사용자 정의 영역의 Layout을 설정합니다.<br/>**참고** : `Paging,Paging2` 는 `SearchMode:1,4,5` 에서 동작 합니다.<ul><li>**Paging** : 페이지 네비게이션 활성화(예약어), 천단위로 ',' 찍힘. ex) `1/1,000`<br/>![Paging](/assets/imgs/Paging.png "Paging")</li><li>**Paging2**: 숫자형 페이지 네비게이션 활성화(예약어), `주의`: Paging과 동시 사용 X<br/>![Paging2](/assets/imgs/paging2.png "Paging2")</li><li>**Count**: 건수 정보 표시(예약어)<br/>![Count](/assets/imgs/Count.png "Count")</li><li>**SummaryLabel** : 선택 영역에 대한 합계/평균 정보 표시<br/>![Paging](/assets/imgs/summaryLabel.png "Paging")</li><li>**StatusLabel** : 데이터 편집, 데이터 조회, 행이동, 필터링, 정렬, 컬럼이동, 파일 업로드/제거 내용 표시<br/>![status](/assets/imgs/statusLabel.png "status")</li><li>**사용자 영역 문자열** : 표시하려는 문자열 \<Span\>\<Div\>와 같은 태그 사용가능</li></ul><br/>(`default: ["Paging","Count"]`)<br/><br/>ex:)<br/>**["Paging",{Value:"\<div style='background-color:#FFFFAA'>1234\</div>",Color:"#FFDDFF"},"가나다","Count"]**<br/>위와 같이 설정시 다음과 같이 표현됩니다.<br/>![InfoRow](/assets/imgs/infoRow0.png "")|
|ViewCount|`number`|Layout의 Paging2 설정시 `PageLength`를 변경하는 selectBox 표시 여부를 결정합니다. `0`:표시안함 (`default`), `1`:표시<br/>![ViewCount](/assets/imgs/viewCount.png "ViewCount")|
|ViewFormat|`string`|Layout의 Paging2 설정 후 `ViewCount:1` 설정시 `ViewCount`의 selectBox 옵션을 설정합니다. "\|" 를 구분자로 구분하며 "10\|20\|30\|40\|50" 과 같이 설정합니다. <br/> ViewFormat을 설정하지 않으면 selectBox 기본 옵션값은 "10\|20\|30\|50\|100"입니다. <br/> 시트의 `PageLength`가 옵션에 포함되어 선택 됩니다.(PageLength가 ViewFormat 문자열에 포함되어 있지 않는 경우 자동 추가 후 선택)
|Paging2Count|`number`|Layout의 Paging2 설정시 페이지 네비게이션에 보여지는 숫자의 개수를 설정합니다. (`default: 5, max: 10`)|
|Space|`string`|정보 행의 위치 ("Top": 상단, "Bottom":하단) (`default: "Bottom"`)|
|Format|`string`|위 `Layout` 에서 `Count`로 설정한 셀(건수정보)에 들어갈 예약어 조합<br/>`default: [BOTTOMDATAROW / TOTALROWS]`<br/><ul><li>TOTALROWS: (서버페이징) 전체 데이터 개수</li><li>ROWCOUNT: 조회된 데이터 개수</li><li>VISIBLECOUNT: 보이는 데이터 개수</li><li>ADDROWS: 추가된 데이터 개수</li><li>CHANGEROWS: 변경된 데이터 개수</li><li>DELETEROWS: 삭제된 데이터 개수</li><li>BOTTOMDATAROW: 현재 가장 마지막에 보이는 행의 번호</li></ul>|

![InfoRowConfig](/assets/imgs/infoRow1.png "InfoRowConfig")

### Example
```javascript
// Html
options.Cfg = {
    InfoRowConfig: {
        "Visible": true,
        "Layout": [
            "Paging", // 예약어 페이지네이션
            {Value:"2024/01/05일 마감 예정입니다.", TextColor:"#FF0000"}, // 임의의 셀
            "Count" // 예약어 건수정보
        ],
        "Space": "Bottom", // InfoRow 상/하 위치
        "Format": "CHANGEROWS개 행이 수정되었습니다." // 건수정보 포멧
    }
 };

 // Layout의 Paging2 는 아래와 같이 설정합니다.
 options.Cfg = {
    InfoRowConfig: {
        "Visible": true,
        "Layout": [
            "Paging2", // 예약어 페이지네이션
            {Value:"2024/01/05일 마감 예정입니다.", TextColor:"#FF0000"}, // 임의의 셀
            "관리자 홍길동", // 임의의 셀2
            "Count" // 예약어 건수정보 
        ],
        "ViewCount": 1, // selectBox 표시
        "ViewFormat": "10|20|30|40|50", // selectBox option 구성
        "Paging2Count": 8, // 페이지 네비게이션에 표시되는 페이지 number 개수
        "Space": "Bottom" // InfoRow 상/하 위치
    }
 };
// InfoRow에 버튼 셀 생성하기
options.Cfg = {
    InfoRowConfig: {
        "Visible": true,
        "Layout": [
            // 버튼 셀 정보 설정
            {Value:"확인", Type:"Button",TextColor:"#FFFFFF", Color:"#53629E", RelWidth:0, Width: 100, OnClick: function(){alert("확인");}},
            "Count"
        ],
        "Space": "Top"
    }
};

// InfoRow 셀에 Formula 적용 (계산 값 표시)
// Layout에 추가한 임의의 셀은 내부적으로 CustomCells1, CustomCells2 ... 로 생성됩니다.
options.Cfg = {
    InfoRowConfig: {
        "Visible": true,
        "Layout": [
            // CustomCells1 로 생성됨 — 체크된 행 수를 표시
            {Align:"left", Formula:function(fr){ return fr.Sheet.getRowsByChecked("sCheck").length + " 건 체크"; }},
            "Count"
        ]
    }
};
```

### Try it
- [Demo of InfoRowConfig](https://jsfiddle.net/gh/get/library/pure/ibsheet/ibsheet8-manual-sample/tree/master/samples/properties/Cfg/InfoRowConfig/)

### Read More
- [SearchMode cfg](/docs/props/cfg/search-mode)
- [SelectionSummary cfg](/docs/props/cfg/selection-summary)
- [setInfoRow method](/docs/funcs/core/set-info-row)
- [setCountInfoElement method](/docs/funcs/core/set-count-info-element)
- [setSelectionSummaryInfoElement method](/docs/funcs/core/set-selection-summary-info-element)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.0.0.5|InfoRow에 Layout.Cells(개별 셀 속성 설정) 기능 추가|
|core|8.1.0.96|StatusLabel 추가|
|core|8.1.0.97|Paging2,ViewCount,ViewFormat,Paging2Count 추가|
