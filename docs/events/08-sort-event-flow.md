# 컬럼 소팅(정렬) 이벤트 발생 순서 ***(event flow)***

> 컬럼 헤더 클릭 또는 doSort() 함수 호출 시 이벤트 발생 순서입니다.

### 헤더 클릭

[onMouseDown](/docs/events/on-mouse-down) → [onMouseUp](/docs/events/on-mouse-up) → [onClick](/docs/events/on-click) → [onBeforeSort](/docs/events/on-before-sort) → [onAfterClick](/docs/events/on-after-click) → (데이터 정렬) → [onAfterSort](/docs/events/on-after-sort)

> 정렬은 비동기로 처리되어 `onAfterSort`는 클릭 흐름(`onAfterClick`)이 끝난 뒤에 발생합니다.

### doSort() 함수 호출

헤더 아이콘 변경 후 데이터 정렬 → [onAfterSort](/docs/events/on-after-sort)

### 이벤트별 시점 및 용도

| 이벤트 | 시점 | 용도 |
|--------|------|------|
| [onBeforeSort](/docs/events/on-before-sort) | 정렬 전 | 정렬 취소 (return -1), 아이콘만 변경 (return 1) |
| [onAfterSort](/docs/events/on-after-sort) | 정렬 완료 후 | 정렬 후 처리 |

### Read More
- [SortCurrentPage cfg](/docs/props/cfg/sort-current-page)
- [ScrollPagingServerSort cfg](/docs/props/cfg/scroll-paging-server-sort)
