# OnAI ***(static)***

<!-- synonyms: static, 전역 함수, IBSheet 정적, 범용 이벤트, OnAI, AI 응답, ai success, AI 요청 성공, AISheetSense 이벤트, AI 이벤트, grid-actions, summary, formula, analyze, script -->

> [AISheetSense](/docs/props/cfg/ai-sheetsense) 의 AI 요청이 **성공**했을 때 발생하는 이벤트입니다.
> 서버 응답 JSON 전체를 전달받아 로깅하거나 추가 후처리를 할 수 있습니다.<br/>
> <mark>AISheetSense 전용 범용 이벤트로, `IBSheet` 객체에 직접 설정하며 모든 시트에 공통 적용됩니다.</mark>

### Syntax
```javascript
IBSheet.OnAI = function(sheet, action, query, response){
    ...
};
```

### Parameters
| Name | Type | Description |
|----------|----|----|
|sheet|`object`|AI 질의가 발생한 시트 객체|
|action|`string`|AI 액션 타입 (아래 표 참고)|
|query|`string`|사용자가 입력한 자연어 질의 문자열|
|response|`object`|서버 응답 JSON 전체 (`_metadata` 포함)<br/>구조는 `action` 에 따라 달라집니다.|

### AI 액션 종류

`action` 은 사용자 질의 내용에 따라 **자동으로 결정**되며, 액션별 `response` 구조는 아래와 같습니다.

|action|설명|response 구조|
|---|---|---|
|`grid-actions`|필터 / 그룹핑 / 정렬 등 시트 제어|`{ actions: [...], suggestions: [...], _metadata: {...} }`|
|`summary`|데이터 요약 및 통계|`{ summary: "...", stats: {...}, suggestions: [...], _metadata: {...} }`|
|`formula`|수식(Formula) 생성|`{ formula: "...", explanation: "...", suggestions: [...], _metadata: {...} }`|
|`analyze`|인사이트 / 이상치 탐색|`{ insights: [...], anomalies: [...], recommendations: [...], _metadata: {...} }`|
|`script`|스크립트 생성|`{ script: "...", description: "...", suggestions: [...], _metadata: {...} }`|

### Return Value
***None***

### Example
```javascript
// AI 요청이 성공했을 때 발생하는 이벤트
IBSheet.OnAI = function(sheet, action, query, response){
    console.log("[AI] Success - action:", action);
    console.log("[AI] Success - query:", query);
    console.log("[AI] Success - response:", response);
};
```

### Read More
- [AISheetSense 설치 및 설정 appendix](/docs/appx/ai-sheetsense-setup)
- [AISheetSense cfg](/docs/props/cfg/ai-sheetsense)
- [OnBeforeAI static](./on-before-ai)
- [OnAIError static](./on-ai-error)

### Since

|product|version|desc|
|---|---|---|
|core|8.4.0.16|기능 추가|
