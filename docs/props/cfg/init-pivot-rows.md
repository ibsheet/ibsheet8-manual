# InitPivotRows ***(cfg)***

<!-- synonyms: InitPivotRows, init pivot rows, pivot row axis, pivot row columns, pivot init rows, 피벗 행, 피벗 세로 기준, 피벗 행 컬럼, 피벗 행 초기값, 초기 피벗 행, 세로 축 컬럼 -->

> 피벗 시트에서 기준 행의 값으로 사용할 열(들)을 설정합니다.
>
> `","`로 연결하여 복수 개의 열 이름을 지정할 수 있습니다.

### Type
`string`


### Example
```javascript
options.Cfg = {
    UsePivot: true, // 피벗 사용 여부
    InitPivotRows: "sDept" // 세로 기준 컬럼 설정
};
```

### Read More
- [UsePivot cfg](./use-pivot)
- [PivotFunc cfg](./pivot-func)
- [InitPivotCols cfg](./init-pivot-cols)
- [InitPivotData cfg](./init-pivot-data)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.6|기능 추가|
|dialog|8.0.0.4|기능 추가|
