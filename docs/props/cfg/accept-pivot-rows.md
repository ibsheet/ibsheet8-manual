# AcceptPivotRows ***(cfg)***

<!-- synonyms: AcceptPivotRows, accept-pivot-rows, 피벗 기준 행, 피벗 행 지정, 피벗 로우, 피벗 사용 행, 피벗 헤더 행, 피벗 그룹 행, 피벗 활성 행, pivot rows, pivot allowed rows, pivot row whitelist, pivot row config -->

> 피벗 시트에서 기준 행의 값으로 사용될 수 있는 열을 설정합니다.
> 복수 개의 열 이름은 `","`로 연결하여 지정할 수 있습니다.

### Type
`string`


### Example
```javascript
options.Cfg = {
    UsePivot: true, // 피벗 사용 여부
    AcceptPivotRows: "sDept,sTeam,sPosition,sName,sGender,sAgeRange,sAddr,sAge,sPeriod"
};
```

### Read More
- [UsePivot cfg](./use-pivot)
- [PivotFormat cfg](./pivot-format)
- [PivotFunc cfg](./pivot-func)
- [AcceptPivotCols cfg](./accept-pivot-cols)
- [AcceptPivotData cfg](./accept-pivot-data)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
