# FocusedCol ***(cfg)***

> 시트를 생성하거나 `reload` 할 때 포커스를 줄 열이름(`ColName`)을 설정합니다.


### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`string`|포커스를 줄 열이름|


### Example
```javascript
options.Cfg = {
    FocusedRow: "AR5",         // 데이터 다섯번째 행에 포커스 처리
    FocusedCol: "sawonName"    // 포커스된 행의 "sawonName" 열에 포커스 처리
};
```

### Read More
- [FocusedRow cfg](./focused-row)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
