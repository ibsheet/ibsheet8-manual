# CanEdit ***(cfg)***

<!-- synonyms: CanEdit, editable, read only, sheet edit, global edit lock, edit lock, 편집 가능, 편집 불가, 읽기 전용, 조회 전용, 편집 잠금, 전체 편집 제어, 편집 허용 여부, sheet readonly, 시트 편집 -->

> 전체 시트의 셀 값 편집(edit) 가능 여부를 설정합니다.  
> 조회 전용 화면 구성 또는 전체 수정 잠금(global edit lock) 처리 시 사용합니다.  
> `CanEdit`이 `1`이 아닌 경우 `Row`, `Col`, `Cell` 단위의 `CanEdit` 설정은 적용되지 않습니다.  
> `필터`, `그룹행`은 해당 속성의 영향을 받지 않습니다.  
> `Button` 타입 클릭 동작과 `File` 타입 아이콘 표시 여부는 이 속성의 영향을 받지 않습니다.  
> ([Disabled col](/docs/props/col/disabled) 을 통해 제어할 수 있습니다.) 

### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`0`|편집 불가<br/>- 편집 불가 상태 배경색 표시 (`ColorState` 8번 설정 적용)<br/>- `Enum`, `Date` 아이콘 미표시<br/>- 데이터 복사 가능|
|`1`|전체 편집 가능 (`default`)|
|`2`|편집 불가<br/>- 배경색 표시 없음<br/>- `Enum`, `Date` 아이콘 표시<br/>- 셀 일부 선택/복사 가능|
|`3`|편집 불가<br/>- 배경색 표시 없음<br/>- `Enum`, `Date` 아이콘 미표시<br/>- 데이터 복사 가능|
|`4`|편집 불가<br/>- 배경색 표시 없음<br/>- `Enum`, `Date` 아이콘 표시<br/>- 데이터 복사 가능|

### Example
```javascript
options.Cfg = {
   "CanEdit":0 
};
```

### Read More
- [ColorState cfg](/docs/props/cfg/color-state)
- [CanEdit row](/docs/props/row/can-edit)
- [CanEdit col](/docs/props/col/can-edit)
- [CanEdit cell](/docs/props/cell/can-edit)
- [Disabled col](/docs/props/col/disabled)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.0.0.12|`CanEdit: 4` 추가|