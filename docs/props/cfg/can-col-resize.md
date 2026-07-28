# CanColResize ***(cfg)***
> 헤더 영역에서 컬럼 경계선을 드래그하여 열 너비를 조정(column width)할 수 있는지 여부를 설정합니다.  
>`Cfg.CanColResize`가 `false`이면 `Col.CanResize` 설정과 관계없이 열 너비 조정은 불가능합니다.   
> 전역에서 비활성화된 경우 하위 단위에서 활성화할 수 없습니다.

<!-- synonyms: resize column, column width, drag column border, adjust column size, drag header border, 열 너비 조정, 컬럼 크기 조절 -->


### 참고

- 데이터가 많거나 병합된 헤더 구조가 복잡한 경우,  
  열 너비 조정 시 화면 재렌더링으로 인해 일시적인 지연이 발생할 수 있습니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0` (`false`)|열 너비 조정 불가|
|`1` (`true`)|열 너비 조정 가능 (`default`)|


### Example
```javascript
options.Cfg = {
    CanColResize: false // 헤더에서 열 너비 조정 불가
};
```

### Read More
- [CanResize col](/docs/props/col/can-resize)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
