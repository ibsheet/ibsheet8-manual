# AISheetSense ***(cfg)***

<!-- synonyms: AI, AISheetSense, 자연어, 챗봇, chat, ibsheet-ai-sheetsense-1.0.0.jar, AI 서버모듈
-->

> IBsheet8 에서 LLM Provider (Openai, Claude, Ollama) 를 활용해 자연어 질의 기능을 이용할 수 있는 챗 다이얼로그를 생성합니다.
> 시트의 데이터 분석/요약/이상치 탐색이나 필터, 그룹핑, 정렬, Formula(수식 적용 )등 시트 기능을 자연어 질문을 통해 확인하고 제어 할 수 있습니다.
> `주의` 해당 기능은 서버모듈 적용이 필요한 기능입니다. (`ibsheet-ai-sheetsense.jar`, `ai-gateway.properties`)

### Type
`boolean`

### Example
```javascript
  // AISheetSense 사용 설정
  options.Cfg = {
    AISheetSense: 1,  // AI 챗 다이얼로그 생성
    AIUrl: './api/ai' // 서버 모듈 설정 경로 (기존의 Cfg.Export.Url 과 동일한 경로 설정)
  };

  // AISheetSense 범용 이벤트
  // AI 요청을 서버에 보내기 직전에 발생하는 이벤트
  IBSheet.OnBeforeAI = function(sheet, action, query, options) {
    // sheet   - 시트 객체
    // action  - AI 액션 타입  => "grid-actions" | "summary" | "formula" | "analyze" | "script"
    // query   - 사용자 자연어 질의 문자열
    // options - { url, context, sessionId, callback, onError, sync }
    // return false → 요청 취소
    // return {object} → options 를 반환된 객체료 교체 후 진행
    console.log("[AI] Before - action:", action, " options:", options);
  };
  // AI 요청 성공했을 때 발생하는 이벤트
  IBSheet.OnAI = function(sheet, action, query, response) {
    // sheet    - 시트 객체
    // action   - AI 액션 타입 => "grid-actions" | "summary" | "formula" | "analyze" | "script"
    // query    - 사용자 자연어 질의 문자열
    // response - 서버 응답 JSON 전체 (_metadata 포함)
    // response 구조 (action별)
    // grid-actions → { actions: [...], suggestions: [...], _metadata: {...} }
    // summary → { summary: "...", stats: {...}, suggestions: [...], _metadata: {...} }
    // formula → { formula: "...", explanation: "...", suggestions: [...], _metadata: {...} }
    // analyze → { insights: [...], anomalies: [...], recommendations: [...], _metadata: {...} }
    // script → { script: "...", description: "...", suggestions: [...], _metadata: {...} }
    console.log("[AI] Success - action:", action, " response:", response);
  };
  // AI 요청 에러시 발생 이벤트
  IBSheet.OnAIError = function(sheet, action, query, error) {
    // sheet  - 시트 객체
    // action - AI 액션 타입 => "grid-actions" | "summary" | "formula" | "analyze" | "script"
    // query  - 사용자 자연어 질의 문자열
    // error  - 에러 정보 (타입이 상황마다 다름)
    // error 발생 케이스
    // 1. URL 미설정 혹은 잘못된 설정 : | "String" | "AI URL not configured" |
    // 2. HTTP 오류                   : | "Number"(음수) | -429 (토큰한도초과) |
    // 3. JSON 파싱 실패              : | Error 객체 | SyntaxError 
    console.error("[AI] Error - action:", action, " error:", error);
  };
```

### Read More
- [Export.Url cfg](../cfg/export)

### Since

|product|version|desc|
|---|---|---|
|core|8.4.0.16|기능 추가|