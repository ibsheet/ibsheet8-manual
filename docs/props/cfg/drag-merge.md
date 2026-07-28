# DragMerge ***(cfg)***

> 병합된 셀을 드래그 시, 첫번째 행과 전체 행의 대상 여부를 선택합니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|드래그 한 셀에 병합된 영역 중 첫번째 행만 (`default`)|
|`1(true)`|드래그 한 셀에 병합된 영역의 전체 행|

### Example
```javascript
options.Cfg = {
    "DragMerge": true
};
```

### Read More

- [CanDrag cfg](./can-drag)
- [DragObject cfg](./drag-object)

### Since

|product|version|desc|
|---|---|---|
|core|8.2.0.26|기능 추가|
