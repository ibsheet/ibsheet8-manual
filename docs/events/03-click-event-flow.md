# 마우스 클릭 이벤트 발생 순서 ***(event flow)***

<!-- synonyms: 마우스 클릭 이벤트 순서, 클릭 이벤트 흐름, 셀 클릭 흐름, 클릭 이벤트 시퀀스, click event flow, mouse click order, click sequence, onClick 순서 -->

> 데이터 셀 마우스 클릭 시 이벤트 발생 순서입니다.

### 발생 순서

[onMouseDown](/docs/events/on-mouse-down) → [onMouseUp](/docs/events/on-mouse-up) → [onClick](/docs/events/on-click) → [onBeforeFocus](/docs/events/on-before-focus) → 커서 렌더링 → [onFocus](/docs/events/on-focus) → [onAfterClick](/docs/events/on-after-click)

### 이벤트별 시점 및 용도

| 이벤트 | 시점 | 용도 |
|--------|------|------|
| [onMouseDown](/docs/events/on-mouse-down) | 마우스 버튼 누름 | 마우스 동작 감지 |
| [onMouseUp](/docs/events/on-mouse-up) | 마우스 버튼 뗌 | 마우스 동작 감지 |
| [onClick](/docs/events/on-click) | 클릭 | 클릭 이벤트 처리, 취소 (return true) |
| [onBeforeFocus](/docs/events/on-before-focus) | 포커스 이동 전 | 포커스 이동 취소 (return true) |
| [onFocus](/docs/events/on-focus) | 포커스 이동 완료 | 포커스 변경 후 처리 |
| [onAfterClick](/docs/events/on-after-click) | 클릭 완료 후 | 클릭 후 최종 처리 |

### 참고

> 더블클릭 또는 `F2`로 편집모드에 진입하면 `onStartEdit` → `onShowEdit`가 발생합니다.  
> 이후 편집·종료·데이터 변경 흐름은 [셀 편집 이벤트 흐름](/docs/events/05-edit-event-flow)을 참고하세요.

### Read More
- [셀 편집 이벤트 흐름](/docs/events/05-edit-event-flow)
