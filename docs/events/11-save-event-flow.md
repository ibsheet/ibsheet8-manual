# 저장 이벤트 발생 순서 ***(event flow)***

<!-- synonyms: 저장 흐름, 저장 이벤트, save flow, save event order -->

> 저장 관련 함수 호출 시 이벤트 발생 순서입니다.  
> 함수별로 발생하는 이벤트가 다르며, `return true`로 중간 단계에서 저장을 중단할 수 있습니다.

### 발생 순서

[onSave](/docs/events/on-save) → [onValidation](/docs/events/on-validation)(셀별 순회) → [onBeforeSave](/docs/events/on-before-save) → (서버 전송 후 응답 수신) → [onAfterSave](/docs/events/on-after-save)

> 위 순서는 `doSave` 기준입니다.  
> `getSaveJson` / `getSaveString`은 데이터 추출만 하므로 `onValidation`만 발생하고, `applySaveResult`는 `onAfterSave`만 발생합니다.

### 이벤트별 시점 및 용도

| 이벤트 | 시점 | 용도 |
|---|---|---|
| [onSave](/docs/events/on-save) | 호출 시 가장 먼저 | 저장 취소 (return true) |
| [onValidation](/docs/events/on-validation) | 셀별 컬럼 단위 순회 | 사용자 정의 유효성 검사 (return true → 저장 중단) |
| [onBeforeSave](/docs/events/on-before-save) | 데이터 수집 후, 서버 전송 전 | 전송 데이터 확인/수정, 저장 취소 (return true) |
| [onAfterSave](/docs/events/on-after-save) | 서버 응답 수신 후 | 저장 결과 처리 (result, message) |

### Read More
- [doSave method](/docs/funcs/core/do-save)
- [getSaveJson method](/docs/funcs/core/get-save-json)
- [getSaveString method](/docs/funcs/core/get-save-string)
- [applySaveResult method](/docs/funcs/core/apply-save-result)
- [저장 응답 규격](/docs/dataStructure/saving-structure)
- [onSave event](./on-save)
- [onValidation event](./on-validation)
- [onBeforeSave event](./on-before-save)
- [onAfterSave event](./on-after-save)
