# CanMove ***(col)***
> 해당 컬럼의 사용자 열 이동 가능 여부를 설정합니다.   
> 사용자가 헤더 셀을 드래그하여 열의 위치를 변경할 수 있는지 여부를 제어합니다.  
> `Cfg.CanColMove`가 `0`이면 `CanMove` 설정과 관계없이 열 이동은 불가능합니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
| `0` (`false`)   | 열 이동 불가 |
| `1` (`true`)  | 열 이동 가능 (`default`) |

### Example
```javascript
options.Cols = [
  { Header: "이름", Name: "name" },
  { Header: "고정열", Name: "fixedCol", CanMove: 0 } // 해당 컬럼만 이동 불가
];
```

### Read More
- [CanColMove cfg](/docs/props/cfg/can-col-move)
- [moveCol method](/docs/funcs/core/move-col)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
