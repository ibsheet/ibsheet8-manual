# CanSelect ***(cfg)***
> 행 또는 셀의 선택(Selection) 기능 활성화 여부를 설정합니다.  
> 마우스 클릭 또는 드래그를 통한 행/셀 범위 선택에 영향을 줍니다.  
> `CanSelect`가 `false`이면 행 및 셀 선택이 비활성화되며,  
> 범위 선택 및 범위 복사는 불가능합니다.  
> 단, Focus(현재 활성 셀)의 값은 복사할 수 있습니다.
>
> ※ 선택(Selection) 기능과 Focus(현재 활성 셀 또는 행 표시)는 별개의 개념입니다.

![canSelect](/assets/imgs/CanSelect_cfg.png "드래그하여 선택시 선택 가능여부")

<!-- synonyms: CanSelect false, 선택 비활성화, 선택 해제, range selection, drag select -->

### 참고
- `CanSelect`는 선택 기능의 활성화 여부를 제어합니다.
- 선택 단위(셀/행)는 `SelectingCells` 설정에 따라 달라집니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
| `0` (`false`) | 행 및 셀 선택 불가 |
| `1` (`true`)  | 행 및 셀 선택 가능 (`default`) |


### Example
```javascript
options.Cfg = {
  "CanSelect": true,       // 행/셀 선택 기능 활성화
  "SelectingCells": 0,     // 행 단위 선택 모드
};
```

### Read More
- [CanSelect row](/docs/props/row/can-select)
- [CanSelect col](/docs/props/col/can-select)
- [SelectingCells cfg](./selecting-cells)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
