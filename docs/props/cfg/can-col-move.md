# CanColMove ***(cfg)***

> 헤더 셀을 드래그하여 열(Column)의 순서를 변경(column reorder)할 수 있는지 여부를 설정합니다.  
> 열 이동 시 헤더와 데이터 영역이 함께 이동합니다.  
> `Cfg.CanColMove`가 `0`이면 `Col.CanMove` 설정과 관계없이 열 이동은 불가능합니다.  
> 전역에서 비활성화된 경우 하위 단위에서 활성화할 수 없습니다.

<!-- synonyms: column reorder, drag header, move column, column position, 컬럼 이동, 헤더 이동 -->

### Type
`number`

### Options
|Value|Description|
|-----|-----|
| `0`   | 열 이동 불가 |
| `1`   | 열 이동 가능 (`default`) |
| `2`   | 병합된 다중 헤더 내에서만 이동 가능 (헤더 2줄 이상) |

### 참고
- 데이터가 많거나 병합된 다중 헤더 구조가 복잡한 경우,  
  열 이동 시 화면 재렌더링으로 인해 일시적인 지연이 발생할 수 있습니다.


### Example
```javascript
options.Cfg = {
    "CanColMove":0        // 사용자 열 순서 변경 불가
};
```

### Try it
- [Demo of CanColMove](https://jsfiddle.net/gh/get/library/pure/ibsheet/ibsheet8-manual-sample/tree/master/samples/properties/Cfg/CanColMove-2/)

### Read More
- [CanMove col](/docs/props/col/can-move)
- [moveCol method](/docs/funcs/core/move-col)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.2.0.12|`CanColMove: 2` 기능 추가|
