# 저장 응답 규격 ***(save response structure)***

<!-- synonyms: 저장 응답 규격, 서버 응답 형식, 저장 결과 구조, save response, IO Result -->

[doSave](/docs/funcs/core/do-save) 또는 [applySaveResult](/docs/funcs/core/apply-save-result) 호출 시 서버에서 시트로 반환되어야 할 `응답 데이터 형식`을 정의합니다.

## 기본 응답 규격
- 서버에서 클라이언트(시트)로 전달되는 json 구조는 아래와 같습니다.
- `Result` 값은 저장 `성공/실패` 여부를 판단하는 기준으로 사용되며, `0` 이상의 값은 `정상` 저장, 0보다 작은 `음수` 값은 저장 중 `오류`로 처리됩니다.
- `Message` 값은 `Result`에 대한 설명 메시지이며, [onAfterSave](/docs/events/on-after-save) 이벤트의 `result`, `message` 파라미터로 전달됩니다.

```javascript
// 성공
{
    "IO": {
        "Result": 0,
        "Message": "저장 되었습니다."
    }
}

// 실패
{
    "IO": {
        "Result": -100,
        "Message": "처리 중 오류가 발생하였습니다.<br/>관리자에게 문의 바랍니다."
    }
}
```

## 정상/실패 처리 동작
- 저장 결과가 **정상**(`Result >= 0`)인 경우, `Added(입력)`, `Changed(수정)` 상태의 행은 상태만 클리어되고 `Deleted(삭제)` 상태의 행은 제거됩니다.  
  정상 저장 시 메시지 표시가 필요한 경우, [onAfterSave](/docs/events/on-after-save) 이벤트에서 직접 처리할 수 있습니다.
- 저장 결과가 **실패**(`Result < 0`)인 경우, 행 상태는 그대로 유지되며 [doSave](/docs/funcs/core/do-save) 함수는 종료됩니다.
- `IO.Result`가 **실패** 코드(`Result < 0`)이고 `Message`가 있을 경우, 해당 내용을 오류 메세지로 표시합니다 (div 팝업, 줄바꿈은 `<br/>` 사용).
- `Message`가 없는 경우에는 `알 수 없는 오류`로 표시합니다.

## IO/Result 속성 누락 처리
리턴 값에 `IO` 또는 `Result` 속성이 없는 경우 다음 기준에 따라 처리됩니다.

| 리턴되는 결과 | 서버상태 | 처리 형태 |
|---|---|---|
| `IO` 안에 `Result`가 없는 경우 | 200 | 성공으로 판단. [onAfterSave](/docs/events/on-after-save) 이벤트에 result는 `0` 리턴 |
| 결과가 아무것도 없는 경우 | 200 | 실패로 판단. [onAfterSave](/docs/events/on-after-save) 이벤트에 result는 `-5` 리턴 |
| 서버에서 오류가 발생한 경우 | 400 이상의 값 | 실패로 판단. [onAfterSave](/docs/events/on-after-save) 이벤트에 result는 `-3` 리턴 |

## Result 결과 코드

> `-3`, `-5`, `-6`, `-7`은 IBSheet에서 사용하는 시스템 오류 코드입니다.  
> 사용자 정의 오류 코드는 다른 값(예: `-10` 이하)을 권장합니다.

| Result | Description | Message(ko, en.js) |
|---|---|---|
| 0 | 정상 ||
| -3 | 요청 Url이 잘못된 경우나 네트워크 오류 등으로 결과를 받지 못한 경우(404,500등의 에러) | Url의 주소를 찾을 수 없습니다.<br/>(ResultErrNotFound) |
| -5 | 응답 결과가 빈값인 경우 | Url에서 응답이 없습니다.<br/>(ResultErrEmptyResponse) |
| -6 | 연결 시간 초과([Timeout cfg](/docs/props/cfg/timeout) 초과) | 연결시간이 초과됐습니다.<br/>(ResultErrRequestTimeout) |
| -7 | 잘못된 데이터 형식(데이터 이상) | 데이터 형식이 잘못됐습니다.<br/>(ResultErrBadDataFormat) |
| 그외 | 사용자 정의 코드<br/>`IO`에 정의된 내용을 [onAfterSave](/docs/events/on-after-save)의 `result`와 `message` 파라미터에서 확인 가능 ||

### Read More
- [acceptChangedData method](/docs/funcs/core/accept-changed-data)
- [applySaveResult method](/docs/funcs/core/apply-save-result)
- [doSave method](/docs/funcs/core/do-save)
- [getSaveJson method](/docs/funcs/core/get-save-json)
- [getSaveString method](/docs/funcs/core/get-save-string)
- [onAfterSave event](/docs/events/on-after-save)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
