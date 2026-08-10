# 붙여넣기 이벤트 발생 순서 ***(event flow)***

<!-- synonyms: 붙여넣기 이벤트 순서, 붙여넣기 흐름, Ctrl+V 이벤트, 클립보드 붙여넣기, paste event flow, paste sequence, clipboard paste order -->

> 클립보드 붙여넣기(Ctrl+V) 시 이벤트 발생 순서입니다.

### 발생 순서

Ctrl+V → [onBeforePaste](/docs/events/on-before-paste) → 데이터 변경 → [onAfterPaste](/docs/events/on-after-paste)

### 이벤트별 시점 및 용도

| 이벤트 | 시점 | 용도 |
|--------|------|------|
| [onBeforePaste](/docs/events/on-before-paste) | 붙여넣기 전 | 붙여넣기 취소 (return true), 데이터 가공 |
| [onAfterPaste](/docs/events/on-after-paste) | 붙여넣기 완료 후 | 붙여넣기 후 처리 |

### Read More
- [셀 편집 이벤트 흐름](/docs/events/05-edit-event-flow)
