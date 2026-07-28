# AddEdit ***(cell)***

> 행의 상태가 추가([Added](/docs/props/row/added))인 행의 셀 편집([CanEdit](/docs/props/cell/can-edit)) 가능 여부를 설정합니다.
>
> 조회 시에는 편집 불가, 행 추가 후 데이터 편집 가능, 저장 후 편집 불가를 설정하고 싶다면 [ChangeEdit](/docs/props/cell/change-edit) 를 함께 설정해주어야 합니다. 
>
> `주의` 해당 속성을 설정하게 되면, `(Cell,Row,Col)CanEdit` 설정 속성은 무시됩니다.
>
> `주의` 해당 속성을 셀로 설정 시 `(Col)AddEdit` 설정이 있어야 합니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|행의 상태가 Added(추가) 일 경우 해당 셀 편집 불가|
|`1(true)`|행의 상태가 Added(추가) 일 경우 해당 셀 편집 가능|


### Example
```javascript

//addRow 를 통하여 추가된 행에 대해서는 AMT 컬럼의 편집을 막음
options.Cols = [
    ...
    {Type: "Int", AddEdit: 0, Name: "AMT", Width: 120 ...},
    ...
];

// AMT 컬럼의 첫번째 row 셀은 AddEdit:1 로 설정한다.
sheet.setAttribute( sheet.getRowById("AR1"), "AMT", "AddEdit", 0);

```

### Read More
- [CanEdit cell](/docs/props/cell/can-edit)
- [ChangeEdit cell](/docs/props/cell/change-edit)
- [AddEdit col](/docs/props/col/add-edit)


### Since

|product|version|desc|
|---|---|---|
|core|8.2.0.16|기능 추가|