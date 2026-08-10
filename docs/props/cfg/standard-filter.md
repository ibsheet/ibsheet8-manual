# StandardFilter ***(cfg)***

<!-- synonyms: StandardFilter, standard filter, tree filter, tree child filter, tree parent filter, 트리 필터, 트리 하위 노드 필터, 트리 부모 자식 필터링, 트리 필터 결과 표시, 트리 필터 모드 -->

> 트리에서 필터 기능 사용시 하위 노드에 대한 보임 감춤 여부를 설정합니다..

### Type
`number`

### Options
|Value|Description|
|-----|-----|
|0|부모 행부터 자식행 순으로 검색하여 필터링합니다. (찾고자 하는 값을 자식행만 갖고 있는 경우에는 표시되지 않습니다.)|
|1|사용금지 (depreated)|
|2|찾고자 하는 값이 자식행에 있는 경우, 해당 행과, 부모 행을 모두 표시 합니다. (`default`)|
|3|찾고자 하는 값이 자식행에 있는 경우, 해당 행의 부모 행과 자식을 모두 표시 합니다.|


### Example
```javascript
options = {
    Cfg:{
      StandardFilter: 3 // 트리에서 필터기능 사용시 찾은 행의 자식행까지 표시
    },
    Cols: [...]
 };
 
```

### Read More
- [showFilter method](/docs/props/cfg/show-filter)
- [showFilterRow method](/docs/funcs/core/show-filter-row)


### Since

|product|version|desc|
|---|---|---|
|core|8.1.0.47|기능 추가|
