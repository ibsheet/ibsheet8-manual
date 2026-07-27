# HeaderCheckMode ***(cfg)***

<!-- synonyms: 전체 체크 대상, 보이는 행만 체크, 필터링 체크, 숨김 행 제외 체크 -->

> 헤더의 전체 체크 박스([HeaderCheck](/docs/props/col/header-check))가 활성화된 시트에서 헤더의 전체 체크 박스를 클릭 시 체크 대상이 되는 행을 설정합니다.

### Type
`number`

### Options
|Value|Description|
|-----|-----|
| `0` | 시트의 모든 행 체크 (`default`)|
| `1` | 보이는 행만 체크 (필터링/`Visible:0` 행 제외)|

### Example
```javascript
options = {
    Cfg :{
        HeaderCheck: 1,  // Type이 Bool인 열의 헤더에 체크박스를 생성합니다.
        HeaderCheckMode: 1, // 시트에 보이는 행에 대해 체크합니다(필터링되거나, 행이 Visible 0일 때 체크가 되지 않습니다)
        ...
    }
};
```

### Read More
- [HeaderCheck col](/docs/props/col/header-check)
- [HeaderCheck cfg](./header-check)
- [HeaderCheckPageOnly cfg](./header-check-page-only)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
