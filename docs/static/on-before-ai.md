# OnBeforeAI ***(static)***

<!-- synonyms: static, 전역 함수, IBSheet 정적, 범용 이벤트, OnBeforeAI, AI 요청 전, before ai, AI 요청 취소, AISheetSense 이벤트, AI 이벤트 -->

> [AISheetSense](/docs/props/cfg/ai-sheetsense) 챗 다이얼로그에서 사용자가 질의를 입력한 뒤,
> AI 요청을 서버에 보내기 **직전**에 발생하는 이벤트입니다.
> 요청 파라미터(`options`)를 확인하거나 수정할 수 있으며, 요청 자체를 취소할 수 있습니다.<br/>
> <mark>AISheetSense 전용 범용 이벤트로, `IBSheet` 객체에 직접 설정하며 모든 시트에 공통 적용됩니다.</mark>

### Syntax
```javascript
IBSheet.OnBeforeAI = function(sheet, action, query, options){
    ...
};
```

### Parameters
| Name | Type | Description |
|----------|----|----|
|sheet|`object`|AI 질의가 발생한 시트 객체|
|action|`string`|AI 액션 타입<br/>`grid-actions` \| `summary` \| `formula` \| `analyze` \| `script`<br/>액션별 설명은 [OnAI](./on-ai) 참고|
|query|`string`|사용자가 입력한 자연어 질의 문자열|
|options|`object`|서버로 전송될 요청 정보 (아래 표 참고)|

**options 객체**

| Name | Type | Description |
|----------|----|----|
|url|`string`|AI 요청 전송 경로|
|context|`object`|LLM 에 전달되는 시트 컨텍스트 정보|
|sessionId|`string`|대화 세션 식별자|
|callback|`function`|요청 성공 시 호출되는 콜백|
|onError|`function`|요청 실패 시 호출되는 콜백|
|sync|`boolean`|동기 요청 여부|

### Return Value
***boolean | object***

|Value|Description|
|-----|-----|
|`false`|AI 요청을 취소합니다.|
|`{object}`|인자로 받은 `options` 를 반환한 객체로 **교체**한 뒤 요청을 진행합니다.|
|`none`|`options` 를 그대로 사용하여 요청을 진행합니다.|

### Example
```javascript
// AI 요청을 서버에 보내기 직전에 발생하는 이벤트
IBSheet.OnBeforeAI = function(sheet, action, query, options){
    console.log("[AI] Before - action:", action);
    console.log("[AI] Before - query:", query);
    console.log("[AI] Before - options:", options);
};
```

### Read More
- [AISheetSense 설치 및 설정 appendix](/docs/appx/ai-sheetsense-setup)
- [AISheetSense cfg](/docs/props/cfg/ai-sheetsense)
- [AIUrl cfg](/docs/props/cfg/ai-url)
- [OnAI static](./on-ai)
- [OnAIError static](./on-ai-error)

### Since

|product|version|desc|
|---|---|---|
|core|8.4.0.16|기능 추가|
