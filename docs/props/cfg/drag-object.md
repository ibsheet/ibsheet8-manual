# DragObject ***(cfg)***

<!-- synonyms: DragObject, drag object, drag preview, drag ghost, drag image, drag indicator, 드래그 대상, 드래그 표시, 드래그 미리보기, 드래그 이미지, 드래그 고스트, 드래그 시 표시, 마우스 드래그 이미지, 행 드래그 표시 -->

> 행을 드래그할 때 마우스에 보여질 대상을 선택합니다.

### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`0`|아무것도 보이지 않음|
|`1`|행 DOM 객체 (`default`)|
|`2`|행의 개수를 담고 있는 메시지|

### Example
```javascript
options.Cfg = {
    DragObject: 2
};
```

### Read More

- [CanDrag cfg](./can-drag)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
