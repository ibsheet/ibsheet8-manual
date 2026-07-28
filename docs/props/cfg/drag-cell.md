# DragCell ***(cfg)***

> 드래그 동작 시 셀 단위 드래그 여부를 설정합니다.  
> `cfg.CanDrag`가 `true`인 경우에만 적용됩니다.

## 참고
- 셀 드래그는 **단일 셀 단위**로 동작합니다. 여러 셀을 한 번에 드래그로 이동하는 기능은 제공되지 않습니다.
- 셀 범위 단위로 옮기려면 범위를 선택한 뒤 복사/붙여넣기(`Ctrl + C` / `Ctrl + V`)를 사용하세요.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|행 단위 드래깅 (`default`)|
|`1(true)`|셀 단위 드래깅|


### Example
```javascript
options.Cfg = {
   "CanDrag": true, // 마우스 드래그 이동 허용
   "DragCell": true // 셀 단위 드래그 활성화
};
```

### Read More

- [CanDrag cfg](/docs/props/cfg/can-drag)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.27|기능 추가|
