# Expanded ***(row)***

<!-- synonyms: 트리 접힘, 트리 펼침, expanded, 행 펼침 상태, 행 접힘 상태 -->

> 트리 기능 사용 시 행의 접힘/펼침 여부를 설정합니다.
<!--!
> `[비공개 설명]` (cell) [ExpandedCols](/docs/props/cell/expand-cols), (cell) [ExpandedRows](/docs/props/cell/expand-rows)로 사용하는 접힘/펼침 여부도 설정가능합니다.
!-->

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|접힘|
|`1(true)`|펼침|


### Example
```javascript
//특정행의 접힘여부 확인
var ep = sheet.getAttribute(sheet.getFocusedRow(), null, "Expanded");

//특정행을 펼칩니다. setExpandRow api 사용
sheet.setExpandRow(sheet.getRowByIndex(4), null, 1);
```

### Read More

- [MainCol cfg](/docs/props/cfg/main-col)
- [HaveChild row](/docs/props/row/have-child)
- [getChildRows method](/docs/funcs/core/get-child-rows)
- [getParentRows method](/docs/funcs/core/get-parent-rows)
- [setExpandRow method](/docs/funcs/core/set-expand-row)
- [showTreeLevel method](/docs/funcs/core/show-tree-level)
- [onBeforeExpand event](/docs/events/on-before-expand)
- [onAfterExpand event](/docs/events/on-after-expand)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
