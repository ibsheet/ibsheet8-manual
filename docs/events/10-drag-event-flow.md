# 드래그 앤 드롭 이벤트 발생 순서 ***(event flow)***

<!-- synonyms: 드래그 이벤트 순서, 드래그 앤 드롭 흐름, 행 드래그 셀 드래그, drag and drop flow, drag drop sequence, dnd event order -->

> 드래그 앤 드롭 시 이벤트 발생 순서입니다.
> 드래그 단위에 따라 행 드래그(`CanDrag`)와 셀 드래그(`DragCell`)로 나뉩니다.

### 행 드래그 (순서 변경)

[onMouseDown](/docs/events/on-mouse-down) → [onStartDrag](/docs/events/on-start-drag) → 드래깅 → [onEndDrag](/docs/events/on-end-drag) → [onDragFinish](/docs/events/on-drag-finish)

### 셀 드래그 (`DragCell`)

[onStartDragCell](/docs/events/on-start-drag-cell) → 드래깅 → [onEndDragCell](/docs/events/on-end-drag-cell)

### 시트 간 드래그

다른 시트로 드래그할 때도 이벤트는 모두 **출발 시트에서만** 발생하며, 도착 시트는 `tosheet`으로 확인합니다.

- **행 드래그**: 시트 간 이동에서는 `onEndDrag`와 `onDragFinish` 사이에 `onAfterRowMoveToSheet`가 추가됩니다(같은 시트 내 이동에서는 발생하지 않습니다).  
[onStartDrag](/docs/events/on-start-drag) → [onEndDrag](/docs/events/on-end-drag) → [onAfterRowMoveToSheet](/docs/events/on-after-row-move-to-sheet) → [onDragFinish](/docs/events/on-drag-finish)
- **셀 드래그**: `onStartDragCell → onEndDragCell`로 동일하며, `onEndDragCell`의 `tosheet` / `torow` / `tocol`로 도착 위치를 받습니다.

### 이벤트별 시점 및 용도

| 이벤트 | 시점 | 용도 |
|--------|------|------|
| [onStartDrag](/docs/events/on-start-drag) | 행 드래그 시작 전 | 드래그 취소(return true), 드래그 표시 HTML 지정 |
| [onEndDrag](/docs/events/on-end-drag) | 행 드롭 시점 | 드롭 허용/거부, 드롭 위치 지정 |
| [onAfterRowMoveToSheet](/docs/events/on-after-row-move-to-sheet) | 시트 간 행 이동 후 | 원본 행 처리 결정(이동 / 복사 / 제거) |
| [onDragFinish](/docs/events/on-drag-finish) | 행 드롭 완료 후(가장 마지막) | 대상 시트(`tosheet`) 반영 후 처리 |
| [onStartDragCell](/docs/events/on-start-drag-cell) | 셀 드래그 시작 전 | 드래그 취소(return true), 드래그 표시 HTML 지정 |
| [onEndDragCell](/docs/events/on-end-drag-cell) | 셀 드롭 시점 | 드롭 위치(`tosheet` / `torow` / `tocol`)에 셀 값 반영 |

### Read More
- [CanDrag cfg](/docs/props/cfg/can-drag)
- [DragCell cfg](/docs/props/cfg/drag-cell)
- [onAfterRowMoveToSheet event](/docs/events/on-after-row-move-to-sheet)
