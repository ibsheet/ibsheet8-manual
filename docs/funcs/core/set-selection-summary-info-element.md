# setSelectionSummaryInfoElement ***(method)***

<!-- synonyms: setSelectionSummaryInfoElement, set-selection-summary-info-element, 선택 영역 요약, 합계 평균, 선택 정보, 요약 표시, 셀 개수, 외부 표시, 정보 요소, selection summary, summary info, selection info, display summary, set summary -->

> 선택한 영역의 셀 개수 및 합계/평균 값 정보를 시트 외부의 Dom Element 에 표시합니다.

### Syntax
```javascript
boolean setCountInfoElement ( element, opt );
```

### Parameters
|Name|Type|Required| Description |
|----------|-----|---|----|
|element |`object` \| `string`|<span class='required'>필수</span>| 선택한 영역의 셀 개수 및 합계/평균 값 정보를 표시할 Dom Element 또는 해당 id|
|opt |`object`|<span class='optional'>선택</span>| [SelectionSummary cfg](/docs/props/cfg/selection-summary) 옵션 정보<br/>`Align`, `Width` 제외|

### Return Value
***boolean*** : `true`: 외부의 Dom Element 표시 성공 `false`: 실패

### Example
```javascript
var option = {
    "Mode": "DelRow|AllRange",
    "SumFormat":"#,###개"
}
// id가 'countElem'인 div 에 선택한 영역의 셀 개수 및 합계/평균 값 정보 출력 설정
sheet.setSelectionSummaryInfoElement ( 'countElem' , option  );
sheet.setSelectionSummaryInfoElement ( docuemnt.getElementById('countElem') , option  );
```

### Read More
- [InfoRowConfig cfg](/docs/props/cfg/info-row-config)
- [SelectionSummary cfg](/docs/props/cfg/selection-summary)
- [getSelectionSummaryInfoElement method](./get-selection-summary-info-element)


### Since

|product|version|desc|
|---|---|---|
|core|8.1.0.6|기능 추가|