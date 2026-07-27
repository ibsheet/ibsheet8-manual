# HaveChild ***(row)***

<!-- synonyms: 동적 트리, 대용량 트리, lazy load, 자식 동적 로드, 트리 일부 로드, 트리 부분 조회 -->

> 상위 레벨만 먼저 조회한 후, 자식이 있을 것으로 예상되는 행에 `HaveChild:true`를 설정하면 [MainCol](/docs/props/cfg/main-col) 트리 컬럼에 접힌 트리 아이콘(`+`)이 표시됩니다.  
> 트리 데이터가 많아 한 번에 조회하기 어려운 경우 사용합니다.  
> `+` 아이콘을 클릭하는 시점에 [loadSearchData](/docs/funcs/core/load-search-data) 또는 [doSearch](/docs/funcs/core/do-search)의 `parent` 인자로 부모 행을 지정해 자식을 조회하여 표시합니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|트리 아이콘 생성하지 않음 (`default`)|
|`1(true)`|접힌 트리 아이콘 생성 — 사용자가 펼칠 때 자식 동적 로드|

### Example

자식이 있을 것으로 예상되는 행에 `HaveChild:true`를 설정하면 트리 아이콘만 표시되고, 사용자가 펼치는 시점에 자식을 동적으로 조회해 추가합니다.

```javascript
// 데이터 객체에 직접 표기
sheet.loadSearchData([
    {Dept:"본부장", HaveChild: true},  // 자식 있음 → 트리 아이콘만 노출
    {Dept:"사원X"}                      // 자식 없음
]);

// 또는 동적 설정
sheet.setAttribute(row, null, 'HaveChild', true);
```

#### 패턴 1 — Items 중첩 데이터

서버 응답이 이미 트리 구조(`Items`로 자식 중첩)인 경우, 그대로 `loadSearchData`에 전달합니다.

```javascript
options.Cfg = { MainCol: "Dept" };

options.Events = {
    onRenderFirstFinish: function(evt) {
        // 초기 0~1레벨 데이터 — 1레벨 중 자식이 있는 행은 HaveChild:true
        evt.sheet.loadSearchData([
            {Dept:"본부장", Items:[
                {Dept:"팀장A", HaveChild: true},
                {Dept:"팀장B"}
            ]},
            {Dept:"임원A", Items:[
                {Dept:"팀장X", HaveChild: true}
            ]},
            {Dept:"사원X"}
        ]);
    },
    onBeforeExpand: function(evt) {
        var row = evt.row;
        // 캐시: 이미 자식이 로드된 경우 재조회 안 함
        if (row.childNodes && row.childNodes.length > 0) return;
        // 자식 동적 조회 (서버 호출 또는 미리 준비된 데이터)
        var children = fetchChildren(row);  // 사용자 구현
        evt.sheet.loadSearchData({data: children, parent: row});
    }
};
```

#### 패턴 2 — 평탄 Level 데이터 + convertTreeData

서버 응답이 `Level` 컬럼을 가진 평탄 데이터인 경우, `ibsheet-common.js`가 제공하는 `IBSheet.v7.convertTreeData()`로 Items 구조로 변환 후 로드합니다 ([트리 응답 규격](/docs/dataStructure/tree-structure) 참고).

```javascript
options.Cfg = { MainCol: "Dept" };

options.Events = {
    onRenderFirstFinish: function(evt) {
        // 초기 평탄 데이터 (Level:0=본부장/임원A/사원X, Level:1=팀장)
        var initialFlat = {
            Data: [
                {Level:0, Dept:"본부장"},
                {Level:1, Dept:"팀장A", HaveChild: true},
                {Level:1, Dept:"팀장B"},
                {Level:0, Dept:"임원A"},
                {Level:1, Dept:"팀장X", HaveChild: true},
                {Level:0, Dept:"사원X"}
            ]
        };
        evt.sheet.loadSearchData(IBSheet.v7.convertTreeData(initialFlat));
    },
    onBeforeExpand: function(evt) {
        var row = evt.row;
        if (row.childNodes && row.childNodes.length > 0) return;
        // 자식도 평탄 Level 데이터로 받아 변환 (자식의 Level은 0부터 시작)
        var childFlat = fetchChildren(row);                  // {Data:[{Level:0, ...}]} 형태
        var childTree = IBSheet.v7.convertTreeData(childFlat);
        evt.sheet.loadSearchData({data: childTree, parent: row});
    }
};
```

### Read More

- [MainCol cfg](/docs/props/cfg/main-col)
- [트리 응답 규격](/docs/dataStructure/tree-structure)
- [loadSearchData method](/docs/funcs/core/load-search-data)
- [doSearch method](/docs/funcs/core/do-search)
- [onBeforeExpand event](/docs/events/on-before-expand)
- [setAttribute method](/docs/funcs/core/set-attribute)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.25|기능 추가|
