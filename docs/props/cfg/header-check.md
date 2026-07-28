# HeaderCheck ***(cfg)***

<!-- synonyms: 전체 헤더 체크박스, 모든 Bool 컬럼 체크박스, 일괄 헤더 체크, header check -->

> 시트 생성 시 `Type:"Bool"`인 모든 열의 헤더에 **헤더 전체 체크박스**를 생성합니다.  
> 헤더 전체 체크박스를 클릭하면 해당 열의 모든 셀이 일괄 체크/체크해제됩니다.  
> 특정 열에만 적용하거나 일부 열만 제외하려면 [HeaderCheck col](/docs/props/col/header-check)을 사용하세요. (col 설정이 cfg보다 우선)

### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`0(false)` | 헤더 체크박스 생성 안 함 (`default`)|
|`1(true)` | 헤더 체크박스 생성|

### Example
```javascript
options = {
    Cfg: {
        HeaderCheck: 1   // Bool 타입 모든 열의 헤더에 체크박스 생성
    },
    Cols: [
        // 특정 컬럼만 헤더 체크박스 제외하려면 col 단위로 HeaderCheck: 0 지정
        {Header: {Value: "확인", HeaderCheck: 0}, Type: "Bool", Name: "chk", Width: 60},
        ...
    ]
};
```

### Read More
- [HeaderCheck col](/docs/props/col/header-check)
- [HeaderCheckMode cfg](./header-check-mode)
- [HeaderCheckPageOnly cfg](./header-check-page-only)
- [AllCheckIgnoreEvent col](/docs/props/col/all-check-ignore-event)
- [setAllCheck method](/docs/funcs/core/set-all-check)
- [onCheckAllFinish event](/docs/events/on-check-all-finish)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
