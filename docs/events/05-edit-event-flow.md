# 셀 편집 이벤트 발생 순서 ***(event flow)***

<!-- synonyms: 편집 이벤트 순서, 셀 편집 흐름, 편집 모드 진입, 편집 시작 종료, edit event flow, cell edit sequence, editing order -->

> 셀 편집모드 진입부터 데이터 변경까지의 이벤트 발생 순서입니다.

### 편집모드 진입 → 편집 → 종료

[onStartEdit](/docs/events/on-start-edit) → [onShowEdit](/docs/events/on-show-edit) → 편집 → [onEndEdit](/docs/events/on-end-edit) → [onAfterEdit](/docs/events/on-after-edit) → 데이터 변경

### 데이터 변경

[onBeforeChange](/docs/events/on-before-change) → Col.OnChange → [onAfterChange](/docs/events/on-after-change)

- 같은 값을 입력한 경우: Col.OnSame 발생

### 이벤트별 시점 및 용도

| 이벤트 | 시점 | 용도 |
|--------|------|------|
| [onStartEdit](/docs/events/on-start-edit) | 편집모드 진입 | 편집 취소 (return true) |
| [onShowEdit](/docs/events/on-show-edit) | 편집모드 표시 시 | 편집 시 보이는 값 변경 |
| [onEndEdit](/docs/events/on-end-edit) | 편집 완료 요청 | 편집 취소 (return true) |
| [onAfterEdit](/docs/events/on-after-edit) | 편집모드 종료 후 | 편집 완료 후 처리 |
| [onBeforeChange](/docs/events/on-before-change) | 값 변경 전 | 값 변경 취소 (return true) |
| [onAfterChange](/docs/events/on-after-change) | 값 변경 후 | 변경 후 처리 |

### 참고

> `setValue` 함수로 값을 변경하면 편집모드 이벤트(`onStartEdit` ~ `onAfterEdit`)와 전역 변경 이벤트(`onBeforeChange`, `onAfterChange`)는 발생하지 않습니다.  
> 컬럼에 설정한 [OnChange](/docs/props/event/on-change) 이벤트만 발생합니다.

### Read More
- [setValue method](/docs/funcs/core/set-value)
