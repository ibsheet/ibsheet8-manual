# SelectingCells ***(cfg)***
> 셀 또는 행 단위의 선택 방식(`Selection mode`)을 설정하는 옵션입니다.  
> 선택 결과는 Row/Col/Cell의 `Selected` 속성에 반영됩니다.  
>
> ※ `SelectingCells`는 선택(`Selection`) 모델을 제어하는 옵션입니다.  
> 클릭 시 표시되는 `Focus`(현재 활성 행 또는 셀 표시)와는 별개의 개념입니다.  
>
> 이 설정은 선택 범위뿐 아니라 `CopyCols`, `PasteCols` 동작에도 영향을 줄 수 있습니다.

<!-- synonyms: selecting cells, selection mode, cell selection, row selection, range selection, 선택 방식, 셀 선택, 행 선택, 범위 선택 -->

### Type
`number`

### Options

| Value | Description |
|-------|------------|
| `0` | **행(Row) 단위로만 선택 가능**<br/><br/>- 복수 행 선택은 Shift/Ctrl + 클릭으로 가능합니다.<br/>- 기본적으로 복사/붙여넣기는 행 단위로 동작합니다.<br/>- 단, `CopyCols` / `PasteCols` 설정에 따라 셀 단위로 동작하도록 제어할 수 있습니다. |
| `1` | **셀 단위 선택 가능** (`default`)<br/><br/>선택 상태에 따라 Row의 [Selected](/docs/props/row/selected) 값이 설정됩니다<br/>- 선택된 셀이 없음: `0`<br/>- 모든 셀이 선택됨: `1`<br/>- 일부 셀만 선택됨: `2`<br/>※ 선택된 셀은 `Cell.Selected = 1`로 적용됩니다. |
| `4` | `SEQ` 컬럼 선택 시 `SelectingCells:0`처럼 동작하고,<br/>그 외 컬럼 선택 시 `SelectingCells:1`처럼 동작 |
<!--※ `SelectingCells:2,3` 값은 동작 검증 후 문서화 예정입니다.
|`2`|개별 셀만 선택 가능. Row 내의 모든 셀이 선택된 경우, Row의 `Selected = 1` 를 가지지 않음. <br/>Row 내의 선택된 셀이 없을때, Row의 `Selected = 0` 를 가짐 <br/>Row 내의 일부 셀만 선택된 경우, Row 의 `Selected = 2` 를 가짐. 단, 개별 셀의 `Selected = 1` 로 설정해야 함 |
|`3`|개별 셀과 행/열선택이 상관 없이 독립적으로 선택 가능<br/>Row 내 선택 셀이 없고, Row 도 선택 안된 경우. Row 의 `Selected = 0` <br/>Row 내 선택 셀이 없고, Row가 선택된 경우. Row 의 `Selected = 1` <br/>Row 내 일부 셀이 선택되고, Row가 선택 안된 경우. Row 의 `Selected = 2`. 단, 개별 셀의 `Selected = 1` 로 설정해야 함 <br/>Row 내 일부 셀이나 전체 셀이 선택되고, Row가 선택된 경우. Row 의 `Selected = 3`|
-->


### Example
```javascript
options.Cfg = {
  SelectingCells: 0,     // 개별 셀 선택 불가능
};
```

### Read More

- [CanSelect cfg](./can-select)
- [CopyCols cfg](./copy-cols)
- [PasteCols cfg](./paste-cols)
- [Selected row](/docs/props/row/selected)
- [Selected cell](/docs/props/cell/selected)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
