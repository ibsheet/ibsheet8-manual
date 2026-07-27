# HeaderCheckPageOnly ***(cfg)***

<!-- synonyms: 페이지 체크, 현재 페이지만 체크, 페이지별 체크, 페이징 체크 -->

> [SearchMode](./search-mode):1에서 사용자가 헤더 전체 체크박스를 클릭해 전체 체크할 때, 현재 보이는 페이지의 행만 체크합니다.  
> [setAllCheck](/docs/funcs/core/set-all-check) 메서드 호출에는 적용되지 않으며, 사용자 클릭 액션에만 동작합니다.

### Type
`number`

### Options
|Value|Description|
|-----|-----|
| `0` | 전체 페이지 체크 (`default`)|
| `1` | 현재 페이지만 체크|

### Example
```javascript
options = {
    Cfg: {
        SearchMode: 1,           // 페이징 모드 (이 속성이 동작하기 위한 전제 조건)
        HeaderCheckPageOnly: 1,  // 헤더 체크박스 클릭 시 현재 페이지의 행만 체크
        ...
    },
    Cols: [
        // 헤더 체크박스를 표시할 Bool 컬럼
        {Header: {Value: "확인", HeaderCheck: 1}, Type: "Bool", Name: "chk", Width: 60},
        ...
    ]
};

// 예) 전체 20페이지 중 사용자가 2 페이지를 보고 있을 때 헤더 체크 클릭 시
//   HeaderCheckPageOnly: 0 (기본) → 1~20 페이지의 모든 행이 체크됨
//   HeaderCheckPageOnly: 1       → 현재 보이는 2 페이지의 행만 체크됨
```

### Read More
- [HeaderCheck cfg](./header-check)
- [HeaderCheck col](/docs/props/col/header-check)
- [HeaderCheckMode cfg](./header-check-mode)
- [SearchMode cfg](./search-mode)

### Since

|product|version|desc|
|---|---|---|
|core|8.3.0.26|기능 추가|
