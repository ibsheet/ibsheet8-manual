---
title: on-before-ai-apply-draft
---

# OnBeforeAIApply ***(static)***

<!-- synonyms: OnBeforeAIApply, AI 적용 전, AI 응답 차단, AI 응답 수정, AISheetSense 이벤트, AI 가드, before apply
-->

> LLM 응답을 **시트에 적용하기 직전**에 발생하는 이벤트입니다.
> 응답 내용을 검사해 적용을 취소하거나, 응답을 수정한 뒤 적용되도록 할 수 있습니다.
>
> 시트 이벤트(`options.Events`)가 아니라 `IBSheet` 객체에 직접 설정하는 **범용 이벤트**이며, 모든 시트에 공통으로 적용됩니다.
> [AISheetSense](/docs/props/cfg/ai-sheet-sense) 옵션이 활성화된 경우에만 발생합니다.

### 참고

- [OnBeforeAI](/docs/static/on-before-ai) 가 **요청을 보내기 전** 단계라면, `OnBeforeAIApply` 는 **응답을 받아 시트에 반영하기 전** 단계입니다.
- AI 가 생성한 스크립트나 액션을 사내 정책에 맞춰 한 번 더 걸러내는 용도로 사용합니다.

### Syntax

```javascript
IBSheet.OnBeforeAIApply = function(sheet, action, query, response) { ... };
```

### Parameters

|파라미터|타입|설명|
|---|---|---|
|`sheet`|`object`|IBSheet 인스턴스|
|`action`|`string`|AI 액션 타입 (`"grid-actions"`, `"summary"`, `"formula"`, `"analyze"`, `"script"`, `"chart"` 등)|
|`query`|`string`|사용자가 입력한 자연어 질의|
|`response`|`object`|LLM 이 반환한 전체 응답 JSON 객체|

### Return

|반환값|동작|
|---|---|
|`false`|시트 적용을 **취소**합니다|
|`{object}`|반환된 객체로 응답을 **교체**하여 적용합니다|
|반환값 없음|원본 응답을 그대로 적용합니다 (`default`)|

### Example

**특정 API 호출 차단**
```javascript
  // script action 에서 행 삭제가 포함된 응답을 막습니다
  IBSheet.OnBeforeAIApply = function(sheet, action, query, response) {
    if (action === "script" && response.script && response.script.indexOf("deleteRow") >= 0) {
      alert("삭제 작업은 허용되지 않습니다.");
      return false;   // 차단
    }
  };
```

**응답 내용 확인 후 수정**
```javascript
  // grid-actions 의 highlight 색상을 항상 노란색으로 강제합니다
  IBSheet.OnBeforeAIApply = function(sheet, action, query, response) {
    if (action === "grid-actions") {
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

### Read More
- [AISheetSense cfg](/docs/props/cfg/ai-sheet-sense)
- [OnBeforeAI static](/docs/static/on-before-ai)
- [OnAI static](/docs/static/on-ai)
- [OnAIError static](/docs/static/on-ai-error)

### Since

|product|version|desc|
|---|---|---|
|core|8.4.0.16|기능 추가|
|aiSheetSense|1.0.1|기능 추가|
