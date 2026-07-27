# getChildRows ***(method)***

<!-- synonyms: 자식 행, child rows, descendants, 트리 자식, 손자 행, 자손 행 -->

> 트리 구조에서 특정 부모 행 아래의 자식 행을 배열로 반환합니다.  
> 기본적으로 손자, 증손자까지 모든 자손이 평탄한 배열로 반환됩니다.  
> `maxLevel`로 깊이를 제한해 직계 자식만 가져올 수도 있습니다.  
> 자식이 없으면 빈 배열을 반환합니다.

### Syntax
```javascript
array getChildRows( row, maxLevel );
```

### Parameters
|Name|Type|Required|Description|
|----------|-----|---|----|
|row|`object`|<span class='required'>필수</span>|부모행 [데이터 로우 객체](/docs/appx/row-object)|
|maxLevel|`number`|<span class='optional'>선택</span>|확인할 자식행의 제한 레벨 (지정한 레벨 **미만**까지 반환)<br/>미지정 시 모든 자손 반환|

### Return Value
***array[row object]*** : [데이터 로우 객체](/docs/appx/row-object) 배열. 자식이 없으면 `[]`

### Example
```javascript
// 전체 자식 행 가져오기 (손자 포함)
var childNodes = sheet.getChildRows(sheet.getFirstRow());

// 직계 자식만 가져오기 (손자 제외)
// maxLevel은 "미만"이므로 row.Level + 2를 지정해야 직계 자식(Level + 1)이 포함됩니다.
var row = sheet.getFocusedRow();
var directChildren = sheet.getChildRows(row, row.Level + 2);

// 자식 행 수 확인
console.log("전체 자식 수: " + childNodes.length);
console.log("직계 자식 수: " + directChildren.length);
```

### Read More
- [getParentRows method](./get-parent-rows)
- [setExpandRow method](./set-expand-row)
- [showTreeLevel method](./show-tree-level)
- [HaveChild row](/docs/props/row/have-child)
- [Expanded row](/docs/props/row/expanded)
- [MainCol cfg](/docs/props/cfg/main-col)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.1.0.14|`maxLevel` 기능 추가|
