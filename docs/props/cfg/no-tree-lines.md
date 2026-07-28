# NoTreeLines ***(cfg)***

<!-- synonyms: 트리 연결선, 트리 노드 선, tree lines, 트리 라인 숨김, 트리 디자인 -->

> 트리를 사용하는 시트 생성 시 노드와 노드 사이의 연결선을 표시할지 여부를 설정합니다.  
> `1`로 설정 시 단순한 접기/펼침 버튼 형태로 트리의 노드가 표현됩니다.

###
![NoTreeLines](/assets/imgs/noTreeLines.png "NoTreeLines 사용")<br/>
[NoTreeLines: true]<br/><br/>
![일반트리](/assets/imgs/tree.png "일반 트리")<br/>
[일반트리]


### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|노드 연결 선을 표시 (`default`)|
|`1(true)`|노드 연결 선을 표시하지 않음|


### Example

`MainCol`로 지정한 트리 시트에서 `NoTreeLines`를 함께 설정합니다.

```javascript
options.Cfg = {
    MainCol: "Cls",          // 트리 컬럼
    NoTreeLines: true        // 노드 연결선을 표시하지 않음
};

options.Cols = [
    {Header: "분류", Type: "Text", Name: "Cls"}
];
```

### Read More
- [MainCol cfg](./main-col)
- [TreeCheckSync cfg](./tree-check-sync)
- [HaveChild row](/docs/props/row/have-child)
- [Expanded row](/docs/props/row/expanded)
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
