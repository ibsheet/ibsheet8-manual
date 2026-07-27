# 체크박스 이벤트 발생 순서 ***(event flow)***

<!-- synonyms: 체크 이벤트 흐름, 체크박스 이벤트 순서, 체크 이벤트 플로우, setAllCheck 이벤트, 헤더 체크 이벤트 -->

> `Bool` 타입 셀의 체크/체크해제 시 이벤트 발생 순서를 트리거별로 정리합니다.

### 1. 개별 셀 마우스 클릭

```
onMouseDown → onMouseUp → onClick → onBeforeFocus → onFocus
  → onBeforeChange → onAfterChange → onAfterClick
```

마우스 클릭은 포커스 이동과 값 변경, 클릭 후 처리까지 모두 발생합니다.

### 2. 개별 셀 키보드 (스페이스/엔터)

```
onBeforeChange → onAfterChange
```

키보드 입력은 클릭 이벤트(`onClick`, `onAfterClick`)를 동반하지 않고 값 변경 이벤트만 발생합니다.

### 3. [setCheck](/docs/funcs/core/set-check) 호출 (단일 셀)

```
onBeforeChange → onAfterChange
```

`setCheck`는 `ignoreEvent` 옵션이 없으며 호출 시 항상 위 이벤트가 발생합니다. `onClick`/`onAfterClick`은 코드 호출이라 발생하지 않습니다.

### 4. [setValue](/docs/funcs/core/set-value) 호출

`setValue`는 `onBeforeChange`/`onAfterChange`를 발생시키지 않습니다. 이벤트가 필요하면 [setCheck](/docs/funcs/core/set-check) 또는 [setAllCheck](/docs/funcs/core/set-all-check)를 사용하세요.

### 5. [setAllCheck](/docs/funcs/core/set-all-check) 호출

| 호출 형태 | 발생 이벤트 |
|---|---|
| `setAllCheck(col, val)` 기본 (`ignoreEvent` 기본값 `0`) | `onBeforeCheckAll` → 각 행 `onBeforeChange` → `onAfterChange` → `onCheckAllFinish` |
| `setAllCheck(col, val, 1)` (이벤트 차단) | `onBeforeCheckAll` → 각 행 `onBeforeChange`만 → `onCheckAllFinish` (`onAfterChange` 차단) |

`setAllCheck`는 기본이 "이벤트 발생"이라 `setValue`와 반대입니다.  
`ignoreEvent:1`을 줘도 **`onBeforeChange`는 차단되지 않으며 `onAfterChange`만 차단**됩니다.  
[AllCheckIgnoreEvent](/docs/props/col/all-check-ignore-event) 컬럼 속성은 `setAllCheck` 호출에는 적용되지 않으므로 이벤트 차단은 위의 `ignoreEvent` 인자로만 가능합니다.

### 6. 헤더 전체 체크박스 사용자 클릭

```
onMouseDown → onMouseUp → onClick → onBeforeCheckAll
  → 각 행: onBeforeChange → onAfterChange
onCheckAllFinish → onAfterClick
```

마우스 클릭 이벤트(`onMouseDown`/`onMouseUp`/`onClick`/`onAfterClick`)와 전체 체크 이벤트가 함께 발생합니다.  
[AllCheckIgnoreEvent](/docs/props/col/all-check-ignore-event)`:1`로 설정된 컬럼은 각 행의 `onAfterChange`가 차단됩니다.

### Read More
- [onBeforeCheckAll event](./on-before-check-all)
- [onCheckAllFinish event](./on-check-all-finish)
- [onBeforeChange event](./on-before-change)
- [onAfterChange event](./on-after-change)
- [onClick event](./on-click)
- [onAfterClick event](./on-after-click)
- [setCheck method](/docs/funcs/core/set-check)
- [setAllCheck method](/docs/funcs/core/set-all-check)
- [setValue method](/docs/funcs/core/set-value)
- [AllCheckIgnoreEvent col](/docs/props/col/all-check-ignore-event)
- [HeaderCheck cfg](/docs/props/cfg/header-check)
- [HeaderCheck col](/docs/props/col/header-check)
