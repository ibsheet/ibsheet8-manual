# DebounceRender ***(cfg)***

> `rerender`, `renderBody` 호출 시 debounce를 적용하여 일정 시간 내 반복 호출되는 경우 마지막 1회만 실행합니다.  
> 반복 호출로 인한 중첩 렌더링 및 성능 저하를 방지합니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
| `0` | debounce 미적용 (`default`) |
| `1` | `rerender`, `renderBody` 호출 시 debounce 적용 |

### Example
```javascript
options = {
    Cfg :{
        DebounceRender: 1, // rerender, renderBody 호출 시 debounce 적용
        ...
    }
};
```

### Read More
- [rerender method](/docs/funcs/core/rerender)
- [renderBody method](/docs/funcs/core/renderBody)

### Since

|product|version|desc|
|---|---|---|
|core|8.3.0.38|기능 추가|
