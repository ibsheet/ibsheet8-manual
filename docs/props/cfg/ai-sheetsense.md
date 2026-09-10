# AISheetSense ***(cfg)***

<!-- synonyms: AI, AISheetSense, 자연어, 챗봇, chat, ibsheet-ai-sheetsense.jar, ibsheet-aisheetsense.js, ai-gateway.properties, LLM, GPT, AI 서버모듈, AI 설치
-->

> IBSheet8 에서 LLM Provider(OpenAI, Anthropic Claude) 를 활용해 자연어 질의 기능을 이용할 수 있는 챗 다이얼로그를 생성합니다.
> 시트의 데이터 분석/요약/이상치 탐색이나 필터, 그룹핑, 정렬, Formula(수식 적용) 등 시트 기능을 자연어 질문을 통해 확인하고 제어할 수 있습니다.

> `주의` 이 옵션은 **단독으로 동작하지 않습니다.** 서버 모듈(`ibsheet-ai-sheetsense-x.x.x.jar`), 설정 파일(`ai-gateway.properties`),
> 클라이언트 플러그인(`ibsheet-aisheetsense.js`) 이 함께 설치되어 있어야 하며 LLM Provider 의 API 키가 필요합니다.
> 자세한 내용은 아래 **전제 조건** 을 참고하세요. 

![AISheetSense](/assets/imgs/AISheetSense_cfg.png "AI 챗 다이얼로그")

### 전제 조건

`AISheetSense` 는 서버 모듈이 함께 설치되어야 동작하는 옵션입니다.
아래 3개 파일을 배치하고 WAS 를 재시작해야 챗 다이얼로그가 정상 동작합니다.

**필요 파일**

|파일|배치 위치|역할|
|---|---|---|
|`ibsheet-ai-sheetsense-x.x.x.jar`|`WEB-INF/lib`|AI 요청을 LLM Provider 로 중계하는 서버 모듈|
|`ai-gateway.properties`|`WEB-INF` 직하|LLM Provider / API 키 / 모델 설정 파일|
|`ibsheet-aisheetsense.js`|IBSheet8 `plugins` 폴더|챗 다이얼로그 UI 를 제공하는 클라이언트 플러그인|

**ai-gateway.properties 설정**

함께 제공되는 `ai-gateway.properties.sample` 을 `ai-gateway.properties` 로 복사한 뒤 값을 입력합니다.

```properties
# ai.provider : openai | claude
ai.provider=openai
ai.api-key=발급받은_API_키
ai.model=gpt-4o-mini
```

- API 키는 환경변수 `AI_API_KEY` 로도 설정할 수 있으며, 환경변수가 설정된 경우 **환경변수가 우선 적용**됩니다.
- 설정 파일은 **서버 시작 시 한 번만** 읽습니다. 값을 변경하면 WAS 를 재시작해야 합니다.

**클라이언트 플러그인 로드**

```html
<script src="assets/ibsheet/plugins/ibsheet-aisheetsense.js"></script>
```

**설치 순서**

1. 위 3개 파일을 각 지정 위치에 배치
2. `ai-gateway.properties.sample` → `ai-gateway.properties` 복사 후 Provider / API 키 / 모델 입력
3. HTML 에 클라이언트 플러그인 `<script>` 추가
4. `options.Cfg` 에 `AISheetSense: 1` 설정
5. WAS 재시작

**요구 사양**

|항목|사양|
|---|---|
|IBSheet8 Core|`ibsheet.js` `8.4.0.16` 이상|
|WAS|Tomcat 8.5 / 9 (`javax`) 또는 Tomcat 10 이상 (Jakarta EE)|
|LLM Provider|OpenAI, Anthropic Claude|

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0` (`false`)|AI 챗 다이얼로그 생성 안 함 (`default`)|
|`1` (`true`)|AI 챗 다이얼로그 생성|

### Example

**AISheetSense 사용 설정**
```javascript
  options.Cfg = {
    AISheetSense: 1   // AI 챗 다이얼로그 생성
  };
```

### 관련 이벤트

AI 요청의 전/후 처리는 **AISheetSense 전용 범용 이벤트**로 제어합니다.
시트 이벤트(`options.Events`)가 아니라 `IBSheet` 객체에 직접 설정하며, 모든 시트에 공통 적용됩니다.

```
사용자 질의 입력
  └→ OnBeforeAI      요청 직전 (파라미터 수정 / 요청 취소 가능)
       └→ 서버 모듈(ibsheet-ai-sheetsense.jar) → LLM Provider
            ├→ 성공 → OnAI
            └→ 실패 → OnAIError
```

|이벤트|시점|용도|
|---|---|---|
|[OnBeforeAI](/docs/static/on-before-ai)|요청 전송 직전|요청 파라미터 수정, 특정 액션 차단|
|[OnAI](/docs/static/on-ai)|요청 성공|응답 후처리, 사용 이력 로깅|
|[OnAIError](/docs/static/on-ai-error)|요청 실패|오류 유형별 사용자 메시지 처리|

```javascript
IBSheet.OnBeforeAI = function(sheet, action, query, options){ /* ... */ };
IBSheet.OnAI       = function(sheet, action, query, response){ /* ... */ };
IBSheet.OnAIError  = function(sheet, action, query, error){ /* ... */ };
```

### 제약 사항

- LLM Provider 의 API 키가 필요합니다. (Provider 측 유료 서비스)
- 응답이 `429 insufficient_quota` 인 경우 Provider 계정의 크레딧 잔액을 확인하세요. 
  `OnAIError` 에서 `-429` 로 전달됩니다.
- `CanEdit` 가 `0` 인 보호된 셀은 AI 가 값을 변경할 수 없습니다.
- AI 가 실행하는 시트 API 는 화이트리스트 방식으로 허용된 것만 실행됩니다.
- `ai-gateway.properties` 변경 사항은 WAS 재시작 후 적용됩니다.

### Read More
- [AIUrl cfg](./ai-url)
- [OnBeforeAI static](/docs/static/on-before-ai)
- [OnAI static](/docs/static/on-ai)
- [OnAIError static](/docs/static/on-ai-error)
- [Export.Url cfg](../cfg/export)
- [CanEdit col](/docs/props/col/can-edit)

### Since

|product|version|desc|
|---|---|---|
|core|8.4.0.16|기능 추가|
