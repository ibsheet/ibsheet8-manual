# OnAIError ***(static)***

<!-- synonyms: static, 전역 함수, IBSheet 정적, 범용 이벤트, OnAIError, AI 오류, ai error, AI 요청 실패, 토큰 한도 초과, 429, insufficient_quota, AI URL not configured, AISheetSense 이벤트, AI 이벤트 -->

> [AISheetSense](/docs/props/cfg/ai-sheetsense) 의 AI 요청이 **실패**했을 때 발생하는 이벤트입니다.
> 실패 원인에 따라 `error` 인자의 **타입이 달라집니다.**<br/>
> <mark>AISheetSense 전용 범용 이벤트로, `IBSheet` 객체에 직접 설정하며 모든 시트에 공통 적용됩니다.</mark>

### Syntax
```javascript
IBSheet.OnAIError = function(sheet, action, query, error){
    ...
};
```

### Parameters
| Name | Type | Description |
|----------|----|----|
|sheet|`object`|AI 질의가 발생한 시트 객체|
|action|`string`|AI 액션 타입<br/>`grid-actions` \| `summary` \| `formula` \| `analyze` \| `script`<br/>액션별 설명은 [OnAI](./on-ai) 참고|
|query|`string`|사용자가 입력한 자연어 질의 문자열|
|error|`string` \| `number` \| `Error`|에러 정보. 발생 원인에 따라 타입이 다릅니다. (아래 표 참고)|

### 에러 발생 케이스

|원인|error 타입|error 값 예시|
|---|---|---|
|AI 요청 경로 미설정 또는 잘못된 설정|`string`|`"AI URL not configured"`|
|HTTP 오류|`number` (음수)|`-429` (토큰 한도 초과)|
|JSON 파싱 실패|`Error` 객체|`SyntaxError`|

- `-429` 는 토큰 한도 초과로, LLM Provider 계정의 크레딧 잔액을 확인해야 합니다.

### Return Value
***None***

### Example
```javascript
// AI 요청 에러시 발생하는 이벤트
IBSheet.OnAIError = function(sheet, action, query, error){
    console.error("[AI] Error - action:", action);
    console.error("[AI] Error - query:", query);
    console.error("[AI] Error - error:", error);
    alert("AI 요청 처리 중 오류가 발생했습니다.");
};
```

### Read More
- [AISheetSense cfg](/docs/props/cfg/ai-sheetsense)
- [AIUrl cfg](/docs/props/cfg/ai-url)
- [OnBeforeAI static](./on-before-ai)
- [OnAI static](./on-ai)

### Since

|product|version|desc|
|---|---|---|
|core|8.4.0.16|기능 추가|
