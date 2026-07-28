# CanEdit ***(col)***

> 해당 열의 편집 가능 여부를 설정합니다.  
> 기본값은 `1`이며, 우선순위는 `Cell` > `Row` > `Col` 순으로 적용됩니다.  
> `Cell`에서 `CanEdit: 0`으로 설정된 경우 `Row` 또는 `Col`에서 `1`로 설정해도 해당 셀은 편집할 수 없습니다.  
> `Cfg.CanEdit`이 `1`이 아닌 경우 `Row`, `Col`, `Cell` 단위의 `CanEdit` 설정은 적용되지 않습니다.  
> `Button` 타입 클릭 동작과 `File` 타입 아이콘 표시 여부는 이 속성의 영향을 받지 않습니다.  
> ([Disabled col](/docs/props/col/disabled)을 통해 제어할 수 있습니다.)


### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`0`|열 편집 불가 (읽기 전용)<br/>- 편집 불가 상태 배경색 표시 (`ColorState` 8번 설정 적용)<br/>- `Enum`, `Date` 아이콘 미표시<br/>- 데이터 복사 가능<br/>![CanEdit](/assets/imgs/canEdit0.png "CanEdit")|
|`1`|열 편집 가능 (`default`)<br/>![CanEdit](/assets/imgs/canEdit1.png "CanEdit")|
|`2`|열 편집 불가<br/>- 배경색 표시 없음<br/>- 셀 일부 선택/복사 가능<br/>- `Enum`, `Date` 아이콘 표시<br/>![CanEdit](/assets/imgs/canEdit2.png "CanEdit")|
|`3`|열 편집 불가<br/>- 배경색 표시 없음<br/>- `Enum`, `Date` 아이콘 미표시<br/>- 데이터 복사 가능|
|`4`|열 편집 불가<br/>- 배경색 표시 없음<br/>- `Enum`, `Date` 아이콘 표시<br/>- 데이터 복사 가능|



### Example
```javascript
// AMT 열을 편집 불가로 설정
options.Cols = [

    {Type: "Int", CanEdit: 0, Name: "AMT", Width: 120}
    
];
```

### Read More
- [CanEdit cfg](/docs/props/cfg/can-edit)
- [CanEdit row](/docs/props/row/can-edit)
- [CanEdit cell](/docs/props/cell/can-edit)
- [getCanEdit method](/docs/funcs/core/get-can-edit)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.0.0.12|`CanEdit: 3, 4` 추가|