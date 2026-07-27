# getParentRows ***(method)***

<!-- synonyms: 부모 행, parent rows, ancestors, 조상 행, 상위 행, 트리 부모 -->

> 트리 구조에서 특정 행의 조상 행들(직접 부모, 그 부모, 루트까지)을 배열로 반환합니다.  
> 배열의 첫 번째(`[0]`)는 가장 가까운 부모이고, 마지막은 최상위 루트 행입니다.  
> 최상위 행에서 호출하면 빈 배열을 반환합니다.

### Syntax
```javascript
array getParentRows( row );
```

### Parameters
|Name|Type|Required|Description|
|----------|-----|---|----|
|row|`object`|<span class='required'>필수</span>|기준이 되는 [데이터 로우 객체](/docs/appx/row-object)|

### Return Value
***array[row object]*** : 조상 행 배열 (직접 부모부터 루트까지). 최상위 행이면 `[]`

### Example

트리 구조:

```
본부장 (L0, 루트)         ← parents[2]
└─ 팀장A (L1)             ← parents[1]
   └─ 사원1 (L2)          ← parents[0] (직접 부모)
      └─ 인턴1 (L3)       ← 기준 행 (getParentRows 호출 대상)
```

```javascript
// 가장 깊은 행(인턴1)에서 getParentRows 호출
var internRow = sheet.getRowById("AR4");   // 인턴1 행
var parents = sheet.getParentRows(internRow);

// 결과 배열 — 직접 부모(가까운 순)부터 루트까지 정렬
console.log(parents.length);    // 3
console.log(parents[0].Dept);   // "사원1"   ← 인턴1의 직접 부모
console.log(parents[1].Dept);   // "팀장A"   ← 그 위
console.log(parents[2].Dept);   // "본부장"  ← 루트 (최상위)

// 직접 부모만 필요한 경우
var directParent = parents[0];

// 루트(최상위) 부모만 필요한 경우
var rootParent = parents[parents.length - 1];

// 최상위 행(본부장)에서 호출 시 빈 배열
sheet.getParentRows(sheet.getFirstRow());  // []
```

### Read More
- [getChildRows method](./get-child-rows)
- [setExpandRow method](./set-expand-row)
- [showTreeLevel method](./show-tree-level)
- [HaveChild row](/docs/props/row/have-child)
- [Expanded row](/docs/props/row/expanded)
- [MainCol cfg](/docs/props/cfg/main-col)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
