# GroupSort ***(cfg)***

<!-- synonyms: GroupSort, group sort, sort before group, group after sort, group sort mode, 그룹 정렬, 그룹핑 정렬, 정렬 후 그룹, 그룹 기준 정렬, sort 그룹, 그룹핑 sort 순서 -->

> 그룹핑시 기준컬럼에 대한 정렬 처리 여부를 설정합니다.


### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|0|Sort 처리 없이 현재 상태로 그룹핑|
|1|Sort 처리 후 그룹핑 (`default`)|


### Example
```javascript
options.Cfg = {
    "GroupSort": 0       // 정렬 처리 하지 않고 현재 상태로 그룹핑
};
```

### Read More
- [Group cfg](./group)
- [GroupMain cfg](./group-main)
- [GroupSortMain](./group-sort-main)

### Since

|product|version|desc|
|---|---|---|
|core|8.3.0.35|기능 추가|
