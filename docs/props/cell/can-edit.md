# CanEdit ***(cell)***

> 해당 셀의 편집 가능 여부를 설정합니다.  
> 기본값은 `1`이며, 우선순위는 `Cell` > `Row` > `Col` 순으로 적용됩니다.  
> `Cell`에 설정된 `CanEdit` 값은 `Row` 및 `Col` 설정보다 우선 적용됩니다.   
> `Cfg.CanEdit`이 `1`이 아닌 경우 `Cell`, `Row`, `Col` 단위의 `CanEdit` 설정은 적용되지 않습니다.  
> `Button` 타입 클릭 동작과 `File` 타입 아이콘 표시 여부는 이 속성의 영향을 받지 않습니다.  
> ([Disabled cell](/docs/props/cell/disabled)을 통해 제어할 수 있습니다.)

### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`0`|셀 편집 불가 (읽기 전용)<br/>- 편집 불가 상태 배경색 표시 (`ColorState` 8번 설정 적용)<br/>- `Enum`, `Date` 아이콘 미표시<br/>- 데이터 복사 가능<br/>![CanEdit](/assets/imgs/canEdit0.png "CanEdit")|
|`1`|셀 편집 가능 (`default`)<br/>![CanEdit](/assets/imgs/canEdit1.png "CanEdit")|
|`2`|셀 편집 불가<br/>- 배경색 표시 없음<br/>- 셀 일부 선택/복사 가능<br/>- `Enum`, `Date` 아이콘 표시<br/>![CanEdit](/assets/imgs/canEdit2.png "CanEdit")|
|`3`|셀 편집 불가<br/>- 배경색 표시 없음<br/>- `Enum`, `Date` 아이콘 미표시<br/>- 데이터 복사 가능|
|`4`|셀 편집 불가<br/>- 배경색 표시 없음<br/>- `Enum`, `Date` 아이콘 표시<br/>- 데이터 복사 가능|


### Example
```javascript
// 1. 메서드를 통해 특정 셀 편집 제한 (열 이름: CLS)
sheet.setAttribute(sheet.getRowById("AR9"), "CLS", "CanEdit", 0);

// 2. 객체 접근 방식으로 설정 (열 이름: CLS)
var row = sheet.getRowById("AR10");
row["CLSCanEdit"] = 1;
sheet.refreshCell({ row: row, col: "CLS" });

// 3. 조회 데이터에서 특정 셀 편집 제한 (열 이름: CLS)
{
  "data": [
    { "CLSCanEdit": 0 }
  ]
}
```

### Read More
- [CanEdit cfg](/docs/props/cfg/can-edit)
- [CanEdit row](/docs/props/row/can-edit)
- [CanEdit col](/docs/props/col/can-edit)
- [getCanEdit method](/docs/funcs/core/get-can-edit)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.0.0.12|`CanEdit: 3, 4` 추가|