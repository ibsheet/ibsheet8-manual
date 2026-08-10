# FocusWholeRow ***(cfg)***

<!-- synonyms: FocusWholeRow, focus whole row, row focus, focus row, focus entire row, whole row focus, 행 포커스, 행 전체 포커스, 행 단위 포커스, 셀 포커스 vs 행 포커스, 행 통째 포커스, 로우 포커스 -->

> 시트 셀 선택시 포커스를 해당 셀에만 처리할지 해당 행 전체에 처리할지를 설정합니다.
>
> `제약사항` 해당 기능 사용시 `Lines` 타입 컬럼은 편집 불가 `(CanEdit:0)` 로 설정됩니다.


### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|시트 셀 단위로 포커스 처리 (`default`)|
|`1(true)`|시트 행 단위로 포커스 처리|


### Example
```javascript
options.Cfg = {
    FocusWholeRow: true     // 행단위로 포커스 처리
};
```

### Read More

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
