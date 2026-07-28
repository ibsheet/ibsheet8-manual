# HeaderCheck ***(col)***

<!-- synonyms: 헤더 체크박스, 전체 체크, 일괄 체크, 헤더 전체 선택, header check -->

> `Type:"Bool"`인 특정 열의 헤더에 **헤더 전체 체크박스**를 생성합니다.  
> 이 옵션은 열의 `Header`를 `object` 형태로 지정한 뒤 그 안에 설정합니다(아래 예제 참고).  
> 헤더 전체 체크박스를 클릭하면 해당 열의 모든 셀이 일괄 체크/체크해제됩니다.  
> 모든 `Bool` 타입 열에 일괄 적용하려면 [HeaderCheck cfg](/docs/props/cfg/header-check)를 사용하세요.  
> [HeaderCheck cfg](/docs/props/cfg/header-check)와 함께 설정된 경우, col 설정이 우선 적용됩니다.

### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`0(false)` | 헤더 체크박스 생성 안 함 (`default`)|
|`1(true)` | 헤더 체크박스 생성|

### Example
```javascript
options.Cols = [
    // 이 컬럼 헤더에만 체크박스 생성
    {Header: {Value: "확인", HeaderCheck: 1},
     Type: "Bool", Name: "chk", Width: 60},
    ...
];
```

### Read More
- [HeaderCheck cfg](/docs/props/cfg/header-check)
- [HeaderCheckMode cfg](/docs/props/cfg/header-check-mode)
- [HeaderCheckPageOnly cfg](/docs/props/cfg/header-check-page-only)
- [AllCheckIgnoreEvent col](./all-check-ignore-event)
- [setAllCheck method](/docs/funcs/core/set-all-check)
- [onCheckAllFinish event](/docs/events/on-check-all-finish)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
