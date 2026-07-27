# showTreeLevel ***(method)***

<!-- synonyms: 트리 레벨 표시, 트리 펼침 레벨, tree level expand, 트리 일괄 접기, 트리 일괄 펼치기 -->

> 지정한 레벨만큼 트리를 접거나 펼칩니다.

### Syntax
```javascript
void showTreeLevel( level, ignoreEvent, childMode );
```

### Parameters
|Name|Type|Required| Description |
|----------|-----|---|----|
|level|`number`|<span class='required'>필수</span>|보고자 하는 레벨 값 (최상위 노드는 `1`부터 시작)|
|ignoreEvent|`boolean`|<span class='optional'>선택</span>|이벤트([onBeforeExpand event](/docs/events/on-before-expand), [onAfterExpand event](/docs/events/on-after-expand)) 호출 여부를 설정<br/>`0(false)`:이벤트 호출 (`default`)<br/>`1(true)`:이벤트 호출하지 않음|
|childMode|`number`|<span class='optional'>선택</span>|지정한 레벨의 하위 로우들의 접힘, 펼침 여부를 설정합니다.<br/>`0`:접거나 펼쳐진 내용 유지 (`default`)<br/>`1`:하위 노드 모두 접음<br/>`2`:하위 노드 모두 펼침|

### Return Value
***none***

### Example
```javascript
// 3레벨까지 표시 (4레벨 이상은 화면상 접힘 — 행의 펼침 상태는 유지)
sheet.showTreeLevel(3);

// 최상위 노드(루트)만 표시 (자식은 화면상 접혀 보이지만 펼침 상태는 유지)
sheet.showTreeLevel(1);

// 2레벨까지 펼치되 onBeforeExpand, onAfterExpand 이벤트는 발생시키지 않음
sheet.showTreeLevel(2, 1);

// 3레벨까지 펼치고 그 하위(4레벨 이하)는 행 상태까지 강제로 접음 (childMode:1)
sheet.showTreeLevel(3, 0, 1);
```

### Read More
- [setExpandRow method](./set-expand-row)
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
|core|8.0.0.4|`ignoreEvent` 인자 추가|
|core|8.0.0.7|`childMode` 인자 추가|
