# 키보드 입력 이벤트 발생 순서 ***(event flow)***

> 데이터 셀 키보드 입력 시 이벤트 발생 순서입니다.

### 발생 순서

[onKeyDown](/docs/events/on-key-down) → [onKeyPress](/docs/events/on-key-press) → [onKeyUp](/docs/events/on-key-up)

> `onKeyPress`는 문자키와 숫자키에서만 발생합니다. 방향키처럼 포커스를 이동시키는 키는 `onKeyDown` → `onBeforeFocus` → `onFocus` → `onKeyUp` 순으로 발생합니다.

### 이벤트별 시점 및 용도

| 이벤트 | 시점 | 용도 |
|--------|------|------|
| [onKeyDown](/docs/events/on-key-down) | 키 누름 | 키 입력 감지, 입력 취소 (return true) |
| [onKeyPress](/docs/events/on-key-press) | 키 입력 | 문자 키 입력 처리 |
| [onKeyUp](/docs/events/on-key-up) | 키 뗌 | 키 입력 완료 처리 |

### 참고

> 편집 가능한 셀에서 문자키를 누르면 편집모드로 진입합니다.  
> 편집의 진입, 종료, 데이터 변경 흐름은 [셀 편집 이벤트 흐름](/docs/events/05-edit-event-flow)을 참고하세요.

### Read More
- [셀 편집 이벤트 흐름](/docs/events/05-edit-event-flow)
