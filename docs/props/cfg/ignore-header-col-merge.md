# IgnoreHeaderColMerge ***(cfg)***

> `ColMerge` 속성을 헤더 영역에도 적용할지 여부를 결정합니다.  
> 헤더 셀에 개별적으로 [ColMerge(cell)](/docs/props/cell/col-merge)를 설정하면 컬럼 설정과 다르게 제어할 수도 있습니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`| ColMerge 속성을 헤더 영역에도 적용합니다. |
|`1(true)`| ColMerge 속성을 헤더 영역에 적용하지 않습니다. (`default`)|


### Example
```javascript
options.Cfg = {
    HeaderMerge: 3,
    DataMerge: 3,
    IgnoreHeaderColMerge: false // ColMerge 속성을 헤더 영역에도 적용
};

options.Cols = [
    // IgnoreHeaderColMerge:false에 의해 ColMerge:0이 헤더에도 적용
    {Header: ["분류","대분류"], Name: "cls1", Type: "Text", ColMerge: 0},          // 헤더+데이터 머지 제외
    {Header: ["분류","중분류"], Name: "cls2", Type: "Text"},                        // 헤더+데이터 머지 대상
    // 헤더 셀만 개별 설정 — 컬럼은 ColMerge:1이지만 헤더 첫 행만 머지 제외
    {Header: [{Value:"소분류", ColMerge:0}, {Value:"소분류"}], Name: "cls3", Type: "Text"},
];
```

### Read More
- [HeaderMerge cfg](./header-merge)
- [ColMerge col](/docs/props/col/col-merge)
- [ColMerge cell](/docs/props/cell/col-merge)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
