# 조회 이벤트 발생 순서 ***(event flow)***

<!-- synonyms: 조회 이벤트 순서, 조회 흐름, 이벤트 흐름도, search event order, event flow -->

> 조회 함수([doSearch](/docs/funcs/core/do-search), [loadSearchData](/docs/funcs/core/load-search-data), [doSearchPaging](/docs/funcs/core/do-search-paging)) 호출 시 이벤트 발생 순서입니다.

### 발생 순서

[onSearchStart](/docs/events/on-search-start) → [onReceiveData](/docs/events/on-receive-data) → [onBeforeDataLoad](/docs/events/on-before-data-load) → [onRowLoad](/docs/events/on-row-load)(행마다) → [onDataLoad](/docs/events/on-data-load) → [onSheetFocus](/docs/events/on-sheet-focus) → [onBeforeFocus](/docs/events/on-before-focus) → [onFocus](/docs/events/on-focus) → [onSearchFinish](/docs/events/on-search-finish)

### 이벤트별 시점 및 용도

| 이벤트 | 시점 | row 객체 | 용도 |
|--------|------|---------|------|
| [onSearchStart](/docs/events/on-search-start) | 조회 시작 | X | 조회 취소, 로딩 표시 |
| [onReceiveData](/docs/events/on-receive-data) | 데이터 수신 | X | 서버 응답 데이터 확인/가공 |
| [onBeforeDataLoad](/docs/events/on-before-data-load) | 데이터 파싱 전 | X | 데이터 가공 |
| [onRowLoad](/docs/events/on-row-load) | 행 로드 시 (행마다 발생) | O | 행별 처리<br/>**주의: 조회 성능이 떨어지므로 사용 권장하지 않음** |
| [onDataLoad](/docs/events/on-data-load) | 데이터 파싱 완료 | O | row 객체 접근, 스타일 적용 |
| [onSheetFocus](/docs/events/on-sheet-focus) | 시트에 포커스될 때 | X | 포커스된 시트 확인 (파라미터는 `sheet`만) |
| [onBeforeFocus](/docs/events/on-before-focus) | 포커스 이동 전 | O | 조건부 포커스 제어 (return true 시 포커스 차단) |
| [onFocus](/docs/events/on-focus) | 첫 번째 셀에 자동 포커스 | O | 포커스 불필요 시 [IgnoreFocused](/docs/props/cfg/ignore-focused) 설정 |
| [onSearchFinish](/docs/events/on-search-finish) | 렌더링 완료 | O | 로딩 제거, UI 업데이트 |

### 참고

> 편집모드 상태에서 조회 함수를 호출하면 `onEndEdit`이 먼저 발생합니다.  
> doSearch 함수의 `callback`은 `onSearchFinish` 직전에 호출됩니다.

[(Cfg)IgnoreFocused](/docs/props/cfg/ignore-focused) 값에 따라 조회 후 포커스 이벤트 발생이 달라집니다.

| `IgnoreFocused` | `onSheetFocus` | `onBeforeFocus` | `onFocus` |
|:-:|:-:|:-:|:-:|
| `0` (기본) | O | O | O |
| `1` | X | X | X |
| `2` | X | O | O |

(O = 발생, X = 발생 안 함)

### Read More
- [이벤트 사용법 기초](/docs/events/01-event)
- [doSearch method](/docs/funcs/core/do-search)
- [loadSearchData method](/docs/funcs/core/load-search-data)
- [doSearchPaging method](/docs/funcs/core/do-search-paging)
