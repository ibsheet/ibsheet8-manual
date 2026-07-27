# FocusedRow ***(cfg)***

> 시트를 생성하거나 `reload` 할 때 포커스 시킬 행의 `ID`를 설정합니다.
>
> 데이터행 : `AR1, AR2 (AutoRow :AR + index)` , 솔리드행 : `SR1, SR2 (SolidRow: SR+index)`, 그룹행 : `GR1, GR2 (GroupRow: GR+index)`...
>


### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`string`|RowID [ 데이터행: `AR1(AutoRow +index)` ]|


### Example
```javascript
options.Cfg = {
    FocusedRow: "AR1",     // 데이터 첫번째 행에 포커스 처리
    FocusedCol: "seq"      // 포커스된 행의 "seq" 열에 포커스 처리
};
```

### Read More
- [FocusedCol cfg](./focused-col)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
