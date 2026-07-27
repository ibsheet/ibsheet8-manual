# setExpandRow ***(method)***

<!-- synonyms: 트리 펼치기, 트리 접기, 트리 토글, expand row, collapse row, 그룹 펼치기 -->

> 트리나 그룹 사용 시 특정 행을 접거나 펼칩니다.  
> `expand` 인자로 펼치기, 접기, 토글 동작을 명시하며 기본값(`null`)은 토글입니다.

### Syntax
```javascript
boolean setExpandRow(row, col, expand);
```

### Parameters
|Name|Type|Required|Description|
|----------|-----|---|----|
|row|`object`|<span class='required'>필수</span>|[데이터 로우 객체](/docs/appx/row-object)|
|col|`string`|<span class='optional'>선택</span>|열이름 (`default: null`)|
|expand|`boolean`|<span class='optional'>선택</span>|펼칠지 여부<br>`0(false)`:접기<br>`1(true)`:펼치기<br>`null`:Toggle (`default`)|

### Return Value
***boolean*** : 접거나 펼쳐짐 변경 여부

### Example
```javascript
var row = sheet.getFocusedRow();

// 펼치기
sheet.setExpandRow(row, null, true);

// 접기
sheet.setExpandRow(row, null, false);

// 토글 (현재 상태 반대로)
sheet.setExpandRow(row);

// 그룹에서 특정 컬럼 기준 토글
sheet.setExpandRow(row, "GROUPNM");
```

### Read More
- [showTreeLevel method](./show-tree-level)
- [getChildRows method](./get-child-rows)
- [getParentRows method](./get-parent-rows)
- [Expanded row](/docs/props/row/expanded)
- [HaveChild row](/docs/props/row/have-child)
- [MainCol cfg](/docs/props/cfg/main-col)
- [onBeforeExpand event](/docs/events/on-before-expand)
- [onAfterExpand event](/docs/events/on-after-expand)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.0.0.5|`expand` 인자 추가 및 `col` 인자 <span class='required'>필수</span>에서 <span class='optional'>선택</span>으로 변경|
