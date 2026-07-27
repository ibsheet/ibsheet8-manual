# ChangeEdit ***(cell)***

> 행의 상태가 수정([Changed](/docs/props/row/changed)) 또는 조회인 상태인 행의 셀 편집([CanEdit](/docs/props/cell/can-edit)) 가능 여부를 설정합니다.
>
> 조회 시에는 편집 불가, 행 추가 후 데이터 편집 가능, 저장 후 편집 불가를 설정하고 싶다면 [AddEdit](/docs/props/cell/add-edit) 를 함께 설정해주어야 합니다. 
>
> `주의` 해당 속성을 설정하게 되면, `(Cell,Row,Col)CanEdit` 설정 속성은 무시됩니다. 
>
> `주의` 해당 속성을 셀로 설정 시 `(Col)ChangeEdit` 설정이 있어야 합니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|행의 상태가 Changed(수정) / 조회 일 경우 해당 셀 편집 불가|
|`1(true)`|행의 상태가 Changed(수정) / 조회 일 경우 해당 셀 편집 가능|


### Example
```javascript
// Changed(수정) 또는 조회 행에 대해서는 AMT 컬럼의 편집을 막음
options.Cols = [
    ...
    {Type: "Int", ChangeEdit: 0, Name: "AMT", Width: 120 ...},
    ...
];

// AMT 컬럼의 첫번째 row 셀은 ChangeEdit:1 로 설정한다.
sheet.setAttribute( sheet.getRowById("AR1"), "AMT", "ChangeEdit", 1);
```


### Read More
- [CanEdit cell](/docs/props/cell/can-edit)
- [AddEdit cell](/docs/props/col/add-edit)
- [ChangeEdit col](/docs/props/col/change-edit)


### Since

|product|version|desc|
|---|---|---|
|core|8.2.0.18|기능 추가|