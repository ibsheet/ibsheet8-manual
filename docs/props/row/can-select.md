# CanSelect ***(row)***
> 해당 행의 선택 가능 여부를 설정합니다.  
> 드래그를 통한 범위 선택 시 `CanSelect: 0`으로 설정된 행은 선택 범위에 포함되지 않습니다.

![CanSelect](/assets/imgs/CanSelect_row.png)
> 특정 행에 `CanSelect: 0`을 적용하여 선택 범위에서 제외된 예시

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|해당 행 선택 불가|
|`1(true)`|해당 행 선택 가능 (`default`)|


### Example
```javascript
// 특정 행을 선택 범위에서 제외
var row = sheet.getRowById("AR55");
row["CanSelect"] = 0;
```

### Read More
- [CanSelect cfg](/docs/props/cfg/can-select)
- [CanSelect col](/docs/props/col/can-select)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
