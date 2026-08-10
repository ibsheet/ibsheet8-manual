# CanSort ***(row)***

<!-- synonyms: row can sort, sortable row, tree child sort, row sort enabled, sort exclude, per-row sort, 행 소팅, 정렬 가능, 소팅 허용, 트리 자식 정렬, 정렬 제외, 소팅 여부, CanSort row -->

> 트리사용시 자식행들에 대한 소팅 가능 불가능 여부를 설정합니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|소팅 불가|
|`1(true)`|소팅 가능|


### Example
```javascript
//특정행의 자식행에 대해 소팅을 허용한다.
var row = sheet.getNextSiblingRow(true);
row["CanSort"] = 1;
```

### Read More
- [SortPos row](/docs/props/row/sort-pos)
- [CanSort col](/docs/props/col/can-sort)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
