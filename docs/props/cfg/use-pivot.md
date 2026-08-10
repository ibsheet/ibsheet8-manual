# UsePivot ***(cfg)***

<!-- synonyms: UsePivot, use pivot, pivot enable, pivot mode, pivot table, pivot data sheet, 피벗 사용, 피벗 활성화, 피벗 시트, 피벗 데이터 시트, 피벗 모드, 피벗 테이블 -->

> 현재 시트를 피벗 시트의 데이터 시트로 사용할지 여부를 설정합니다.
>
> 해당 옵션 설정 시 피벗 시트의 행, 열, 데이터로 사용될 열 들을 설정 할 수 있는 행과 피벗 생성 / 삭제등의 컨트롤을 담당하는 행이 [Solid](/docs/appx/solid)영역에 추가됩니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|피벗 사용 안함 (`default`)|
|`1(true)`|피벗 사용|

### Example
```javascript
options.Cfg = {
    UsePivot: true              // 피벗 사용 여부
};
```

### Read More
- [PivotFormat cfg](./pivot-format)
- [PivotFunc cfg](./pivot-func)
- [AcceptPivotRows cfg](./accept-pivot-rows)
- [AcceptPivotCols cfg](./accept-pivot-cols)
- [AcceptPivotData cfg](./accept-pivot-data)
- [Solid appendix](/docs/appx/solid)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
