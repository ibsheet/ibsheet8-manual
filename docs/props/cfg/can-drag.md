# CanDrag ***(cfg)***

> 데이터 행을 마우스로 드래그하여 순서를 변경(row reorder)할 수 있는지 여부를 설정합니다.  
> 단, 고정 행(Header, Head, Foot, 합계, 소계 행 등) 및 그룹 행은 이동할 수 없습니다.

<!-- synonyms: drag row, move row, reorder row, row drag, 행 이동, 순서 변경 -->
## 참고
- 여러 행을 드래그로 이동하려면, 행 단위 선택 모드인 `SelectingCells:0` 설정이 필요합니다.
- 사용자는 드래그 전 `Shift + Click` 또는 `Ctrl + Click`으로 원하는 행들을 선택해야 합니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|마우스 드래그를 통한 행 이동 불가 (`default`)|
|`1(true)`|마우스 드래그를 통한 행 이동 가능|


### Example
```javascript
// 1. 단일 행 드래그 허용
options.Cfg = {
  CanDrag: true
};

// 2. 복수 행 드래그 허용
options.Cfg = {
  CanDrag: true,
  SelectingCells: 0
};
```

### Try it
- [Demo of CanDrag](https://jsfiddle.net/gh/get/library/pure/ibsheet/ibsheet8-manual-sample/tree/master/samples/properties/Cfg/CanDrag-true/)

### Read More
- [CanDrag row](/docs/props/row/can-drag)
- [DragCell cfg](./drag-cell)
- [DragObject cfg](./drag-object)
- [SelectingCells cfg](./selecting-cells)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
