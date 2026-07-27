# TreeCheckSync ***(cfg)***

<!-- synonyms: 트리 체크 동기화, 부모 자식 체크, 트리 체크박스 관계, 부모 자동 체크, 자식 자동 체크 -->

> [MainCol](/docs/props/cfg/main-col) 기반 트리 시트에서 부모/자식 간 체크 동기화 동작을 설정합니다.  
> [Icon](/docs/props/col/icon)이나 [Button](/docs/props/col/button) 속성이 `"Check"`로 설정된 컬럼에 적용됩니다.

### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`0` | 일반 모드 — 부모/자식 관계와 무관하게 각자 체크|
|`1` | 관계 모드 — 부모/자식 자동 동기화, 자식이 일부만 체크되면 부모 체크박스에 `?` 표시 (`default`)|
|`2` | 관계 모드 — 부모/자식 자동 동기화, 자식이 일부만 체크되면 부모 체크박스에 `v` 표시|

자식 노드(콩류) 하나를 체크했을 때 부모의 표시 차이:

![TreeCheckSync: 0](/assets/imgs/treeCheckSync-0.png "0 — 일반 모드, 부모는 영향 받지 않음")
![TreeCheckSync: 1](/assets/imgs/treeCheckSync-1.png "1 — 자식 일부 체크 시 부모에 ? 표시")
![TreeCheckSync: 2](/assets/imgs/treeCheckSync-2.png "2 — 자식 일부 체크 시 부모에 v 표시")

### Example

`MainCol`로 지정한 트리 컬럼에 `Icon:"Check"`로 체크박스를 표시한 뒤 `TreeCheckSync`로 동기화 동작을 설정합니다.

```javascript
options.Cfg = {
    MainCol: "Cls",        // 트리 컬럼
    TreeCheckSync: 1       // 부모/자식 체크 동기화 (자식 일부 체크 시 부모에 '?' 표시)
};

options.Cols = [
    {
        Header: "분류",
        Type: "Text",
        Name: "Cls",
        Icon: "Check"      // 트리 컬럼에 체크박스 표시 — TreeCheckSync 동작 대상
    }
];
```

### Read More
- [MainCol cfg](/docs/props/cfg/main-col)
- [Icon col](/docs/props/col/icon)
- [Button col](/docs/props/col/button)
- [Checked cell](/docs/props/cell/checked)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.4|기능 추가|
|core|8.2.0.2|2 mode 추가|
