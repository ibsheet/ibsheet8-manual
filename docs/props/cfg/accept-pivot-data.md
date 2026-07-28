# AcceptPivotData ***(cfg)***

> 피벗 시트에서 데이터의 값으로 사용될 수 있는 열을 설정합니다.
> 복수 개의 열 이름은 `","`로 연결하여 지정할 수 있습니다.

### Type
`string`

### Example
```javascript
options.Cfg = {
    UsePivot: true, // 피벗 사용 여부
    AcceptPivotData: "sAge,sPeriod,sSalary,sBonus"
};
```

### Read More
- [UsePivot cfg](./use-pivot)
- [PivotFormat cfg](./pivot-format)
- [PivotFunc cfg](./pivot-func)
- [AcceptPivotCols cfg](./accept-pivot-cols)
- [AcceptPivotRows cfg](./accept-pivot-rows)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
