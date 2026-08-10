# HeaderSortActionMode ***(cfg)***

<!-- synonyms: HeaderSortActionMode, header sort action mode, header click sort, ctrl click sort, multi sort click, single sort click, 헤더 정렬 동작, 헤더 클릭 정렬, Ctrl 클릭 정렬, 다중 정렬, 단일 정렬, 다중 소팅, 단일 소팅, 헤더 소팅 방식 -->

> 헤더 클릭/Ctrl 클릭 시 어떻게 소팅할지 결정합니다.</br>
> 옵션에 따라 단일 열에 대한 소팅과 다중 열에 대한 소팅이 실행됩니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
| `0(false)` | 클릭 시 다중 소팅을 사용하며, Ctrl 클릭 시 단일 소팅을 사용합니다. (`default`)|
| `1(true)` | 클릭 시 단일 소팅을 사용하며, Ctrl 클릭 시 다중 소팅을 사용합니다.|

### Example
```javascript
options.Cfg = {
    HeaderSortActionMode: true,
    ...
};
```

### Read More
- [MaxSort cfg](/docs/props/cfg/max-sort)
- [HeaderSortMode cfg](/docs/props/cfg/header-sort-mode)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.5|기능 추가|
