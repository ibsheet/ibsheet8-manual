# 기타 이벤트 발생 순서 ***(event flow)***

> 개별 흐름도로 두기엔 짧은 이벤트들의 발생 순서입니다. 필터 편집, 그룹핑, 컨텍스트 메뉴를 다룹니다.

## 필터 편집

[doFilter](/docs/funcs/core/do-filter) 호출 또는 필터행([showFilterRow](/docs/funcs/core/show-filter-row))에서 필터 값 변경 → [onBeforeFilter](/docs/events/on-before-filter) → [onReadFilteringValue](/docs/events/on-read-filtering-value) (대상 열의 셀마다) → [onRowFilter](/docs/events/on-row-filter) (행마다) → (필터 적용·렌더링) → [onAfterFilter](/docs/events/on-after-filter)

### 이벤트별 시점 및 용도

| 이벤트 | 시점 | 용도 |
|--------|------|------|
| [onBeforeFilter](/docs/events/on-before-filter) | 필터 전 | 필터 취소 (return `1`) |
| [onReadFilteringValue](/docs/events/on-read-filtering-value) | 대상 열의 각 셀마다 | 실제 셀 값 대신 필터에 사용할 값 리턴 (셀 값은 유지) |
| [onRowFilter](/docs/events/on-row-filter) | 각 행마다 | 행 표시 여부(`show`) 리턴 |
| [onAfterFilter](/docs/events/on-after-filter) | 필터 완료 후 | 필터 후 처리 |

## 그룹핑

[doGroup](/docs/funcs/core/do-group) 호출 또는 시트 생성 시 `Cfg`의 `Group` 설정 → [onBeforeGroup](/docs/events/on-before-group) → (데이터 그룹핑) → [onAfterGroup](/docs/events/on-after-group)

### 이벤트별 시점 및 용도

| 이벤트 | 시점 | 용도 |
|--------|------|------|
| [onBeforeGroup](/docs/events/on-before-group) | 그룹 실행/해제 전 | 그룹 취소 (return `1`) |
| [onAfterGroup](/docs/events/on-after-group) | 그룹 실행/해제 후 (렌더링 전) | 그룹 후 처리 |

## 컨텍스트 메뉴

셀에서 마우스 우클릭 → [onReadMenu](/docs/events/on-read-menu) → [onShowMenu](/docs/events/on-show-menu) → (메뉴 표시) → 메뉴 아이템 선택 → [onSelectMenu](/docs/events/on-select-menu)

> [showMenu](/docs/funcs/core/show-menu) 메소드로 생성한 메뉴에는 위 세 이벤트가 발생하지 않습니다. 마우스 우클릭으로 열리는 컨텍스트 메뉴에서만 발생합니다.

### 이벤트별 시점 및 용도

| 이벤트 | 시점 | 용도 |
|--------|------|------|
| [onReadMenu](/docs/events/on-read-menu) | 메뉴 표시 전 | 메뉴를 새로 구성해 리턴 (기존 메뉴 대체) |
| [onShowMenu](/docs/events/on-show-menu) | 메뉴 표시 시 | 메뉴 표시 취소 (return `1`) |
| [onSelectMenu](/docs/events/on-select-menu) | 메뉴 아이템 클릭 시 | 선택한 항목(`result`) 처리 |

### Read More
- [showMenu method](/docs/funcs/core/show-menu)
- [getFilter method](/docs/funcs/core/get-filter)
- [showFilterRow method](/docs/funcs/core/show-filter-row)
