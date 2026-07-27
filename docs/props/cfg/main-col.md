# MainCol ***(cfg)***

<!-- synonyms: 트리 메인 컬럼, tree main column, 트리 열, 트리 접힘/펼침 열, 트리 표시 컬럼 -->

> 트리 기능 사용 시 트리의 노드를 표시하는 열을 설정합니다.  
> 지정한 열에서 트리의 접힘/펼침 아이콘이 보여지게 됩니다.  
> 반드시 하나의 열만 트리가 될 수 있습니다.  
> 트리를 사용할 때는 조회 데이터도 트리에 맞춰서 구성되어야 합니다 ([트리 응답 규격](/docs/dataStructure/tree-structure) 참고).

### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`colName`|트리가 표시될 열이름|


### Example

조회 데이터의 `Items`에 자식 행을 중첩해 한 번에 트리 전체를 로드하는 패턴입니다.

```javascript
options.Cfg = {
    MainCol: "Emp_name"        // 시트 트리를 열이름이 "Emp_name"인 열에 표시
};

sheet.loadSearchData([
    {Emp_name: "본부장", Items: [
        {Emp_name: "팀장A", Items: [
            {Emp_name: "사원1"},
            {Emp_name: "사원2"}
        ]},
        {Emp_name: "팀장B"}
    ]}
]);
```

### Try it
- [Demo of MainCol](https://jsfiddle.net/gh/get/library/pure/ibsheet/ibsheet8-manual-sample/tree/master/samples/properties/Cfg/MainCol/)
- [Demo of Tree Formula (부서별 실적 집계)](https://jsfiddle.net/gh/get/library/pure/ibsheet/ibsheet8-manual-sample/tree/master/samples/properties/Col/Formula-TreeSum/)

### Read More
- [트리 응답 규격](/docs/dataStructure/tree-structure)
- [TreeCheckSync cfg](/docs/props/cfg/tree-check-sync)
- [NoTreeLines cfg](/docs/props/cfg/no-tree-lines)
- [Expanded row](/docs/props/row/expanded)
- [HaveChild row](/docs/props/row/have-child)
- [Formula col](/docs/props/col/formula)
- [getChildRows method](/docs/funcs/core/get-child-rows)
- [setExpandRow method](/docs/funcs/core/set-expand-row)
- [showTreeLevel method](/docs/funcs/core/show-tree-level)
- [onBeforeExpand event](/docs/events/on-before-expand)
- [onAfterExpand event](/docs/events/on-after-expand)
<!--!
- `[비공개]` [ReversedTree cfg](/docs/props/cfg/reversed-tree)
- `[비공개]` [ExpandLevel row](/docs/props/row/expand-level)
!-->


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
