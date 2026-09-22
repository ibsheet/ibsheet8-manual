# OnBeforeAIApply ***(static)***

<!-- synonyms: static, 전역 함수, IBSheet 정적, 범용 이벤트, OnBeforeAIApply, AI 적용 전, before apply, AI 응답 차단, AI 응답 수정, AISheetSense 이벤트, AI 이벤트 -->

> [AISheetSense](/docs/props/cfg/ai-sheetsense) 의 AI 응답을 **시트에 적용하기 직전**에 발생하는 이벤트입니다.
> 응답(`response`) 내용을 확인하거나 수정할 수 있으며, 적용 자체를 취소할 수 있습니다.
> <mark>AISheetSense 전용 범용 이벤트로, `IBSheet` 객체에 직접 설정하며 모든 시트에 공통 적용됩니다.</mark>

### Syntax

```javascript
IBSheet.OnBeforeAIApply = function(sheet, action, query, response){ ... };
```

### Parameters

| Name | Type | Description |
|----------|----|----|
|sheet|`object`|AI 질의가 발생한 시트 객체|
|action|`string`|AI 액션 타입 `grid-actions` \| `summary` \| `formula` \| `analyze` \| `script` 액션별 설명은 [OnAI](./on-ai) 참고|
|query|`string`|사용자가 입력한 자연어 질의 문자열|
|response|`object`|LLM 이 반환한 서버 응답 JSON 전체. 구조는 `action` 에 따라 달라집니다.|

### Return Value
***boolean | object***

|Value|Description|
|-----|-----|
|`false`|응답을 시트에 적용하지 않고 **취소**합니다.|
|`{object}`|인자로 받은 `response` 를 반환한 객체로 **교체**한 뒤 적용합니다.|
|`none`|`response` 를 그대로 사용하여 적용합니다.|

### Example

```javascript
  // 예1) script 액션에서 특정 API 호출 차단
  IBSheet.OnBeforeAIApply = function(sheet, action, query, response){
    if (action === "script" && response.script && response.script.indexOf("deleteRow") >= 0) {
      alert("삭제 작업은 허용되지 않습니다.");
      return false;   // 적용 취소
    }
  };
```

```javascript
  // 예2) 응답 내용을 확인한 뒤 수정하여 적용
  IBSheet.OnBeforeAIApply = function(sheet, action, query, response){
    if (action === "grid-actions") {
      // highlight 색상을 항상 노란색으로 강제
      var actions = response.actions || [];
      for (var i = 0; i < actions.length; i++) {
        if (actions[i].type === "highlight") {
          actions[i].color = "#FFFF00";
        }
      }
      return response;   // 수정된 응답으로 적용
    }
  };
```
