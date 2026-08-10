# 트리 확장/접기 이벤트 발생 순서 ***(event flow)***

<!-- synonyms: 트리 이벤트 순서, 트리 확장 접기 흐름, 노드 확장 이벤트, expand collapse 순서, tree event flow, tree expand collapse sequence -->

> 트리 확장/접기 시 이벤트 발생 순서입니다.

### 마우스 사용

[onMouseDown](/docs/events/on-mouse-down) → [onMouseUp](/docs/events/on-mouse-up) → [onClick](/docs/events/on-click) → [onBeforeExpand](/docs/events/on-before-expand) → 동작 완료 → [onAfterExpand](/docs/events/on-after-expand) → [onAfterClick](/docs/events/on-after-click)

<!--
### 키보드 사용 (`Ctrl + Enter`)

[onKeyDown](/docs/events/on-key-down) → [onBeforeExpand](/docs/events/on-before-expand) → 동작 완료 → [onAfterExpand](/docs/events/on-after-expand) → [onKeyUp](/docs/events/on-key-up)
-->

### showTreeLevel() 함수 호출

[onBeforeExpand](/docs/events/on-before-expand) → 동작 완료 → [onAfterExpand](/docs/events/on-after-expand)

### 이벤트별 시점 및 용도

| 이벤트 | 시점 | 용도 |
|--------|------|------|
| [onBeforeExpand](/docs/events/on-before-expand) | 확장/접기 전 | 동작 취소 (return true) |
| [onAfterExpand](/docs/events/on-after-expand) | 확장/접기 완료 후 | 완료 후 처리 |

### Read More
- [MainCol cfg](/docs/props/cfg/main-col)
- [트리 응답 규격](/docs/dataStructure/tree-structure)
