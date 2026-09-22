# AISheetSense 설치 및 설정  ***(appendix)***

<!-- synonyms: AISheetSense, AI 설치, AI 서버모듈, 서버 모듈 설치, 환경 설정, 환경 셋팅, 서버 셋팅, jar 설치, ai-gateway.properties, ibsheet-aisheetsense.js, javax, jakarta, Ollama, vLLM, 로컬 LLM, 폐쇄망, 온프레미스, 자연어 질의, AI 트러블슈팅, token.daily-limit, ai setup -->

> 자연어로 시트를 조회하고 제어하는 [AISheetSense](/docs/props/cfg/ai-sheetsense) 를 사용하기 위한 **서버 환경 셋팅**과 설정 방법을 설명합니다.
> **이 기능은 클라이언트 플러그인만으로는 동작하지 않으며, 서버 모듈을 함께 설치해야 합니다.**

## 지원 환경

|항목|사양|
|---|---|
|IBSheet8 Core|`ibsheet.js` `8.4.0.16` 이상|
|AISheetSense|`1.0.0` 이상|
|WAS|Tomcat 8.5 / 9 (`javax`) 또는 Tomcat 10 이상 (Jakarta EE)|
|JDK|Java 8 이상|
|LLM Provider|OpenAI, Anthropic Claude, Local(Ollama, vLLM 등)|

## 필수 파일

|파일|배치 위치|역할|
|---|---|---|
|`ibsheet-ai-sheetsense-x.x.x.jar`|`WEB-INF/lib`|AI 요청을 LLM Provider 로 중계하는 서버 모듈.<br/>Tomcat 10 이상은 `-jakarta` 빌드를 사용합니다.|
|`ai-gateway.properties`|`WEB-INF` 직하|LLM Provider / API 키 / 모델 설정 파일|
|`ibsheet-aisheetsense.js`|IBSheet8 `plugins` 폴더|챗 다이얼로그 UI 를 제공하는 클라이언트 플러그인|

- 서버 모듈은 WAS 환경에 맞는 **빌드를 하나만** 배치합니다. 맞지 않는 빌드를 넣으면 **오류 메시지 없이 챗 다이얼로그만 표시되지 않습니다.**
- `ai-gateway.properties` 경로는 서버 모듈에 고정되어 있어 변경할 수 없습니다. 하위 폴더나 `classes` 아래에 두면 읽지 못합니다.
- 설정 파일은 배포 파일에 포함된 `ai-gateway.properties.sample` 을 복사한 뒤 이름을 변경해 사용합니다.

## 설치 순서

1. 위 3개 파일을 각 지정 위치에 배치합니다.
2. `ai-gateway.properties.sample` → `ai-gateway.properties` 로 복사한 뒤 Provider / 모델 / (클라우드의 경우) API 키를 입력합니다.
3. AI 기능을 사용할 페이지에 클라이언트 플러그인을 추가합니다. 플러그인은 `ibsheet.js` **다음에** 로드합니다.
   ```html
   <script src="assets/ibsheet/ibsheet.js"></script>
   <script src="assets/ibsheet/plugins/ibsheet-aisheetsense.js"></script>
   ```
4. 시트 생성 옵션에 [AISheetSense](/docs/props/cfg/ai-sheetsense) 를 설정합니다. 서버 모듈 경로를 직접 지정해야 하는 경우 [AIUrl](/docs/props/cfg/ai-url) 을 함께 설정합니다.
   ```javascript
   options.Cfg = {
       AISheetSense: 1
   };
   ```
5. WAS 를 재시작합니다. 설정 파일은 서버 시작 시점에 한 번만 읽으므로, 이후 설정을 변경한 경우에도 재시작이 필요합니다.

## ai-gateway.properties 설정

|키|기본값|설명|
|---|---|---|
|`ai.provider`|`openai`|LLM Provider. `openai` / `claude` / `local`|
|`ai.api-key`| |API 키. `local` 은 필요하지 않습니다|
|`ai.model`|`gpt-4o-mini`|사용할 모델명|
|`ai.api-url`|Provider 별 기본값|API 엔드포인트. 기본값과 다른 주소를 사용할 때만 지정합니다|
|`ai.json-format`|`true`|JSON 응답 형식(`json_object`) 사용 여부|
|`ai.connect-timeout`|`10`|연결 타임아웃(초)|
|`ai.read-timeout`|`60`|응답 대기 타임아웃(초)|
|`cache.enabled`|`true`|동일 질의에 대한 응답 캐시 사용 여부|
|`cache.ttl`|`300`|캐시 유지 시간(초)|
|`cache.max-size`|`200`|캐시 최대 보관 건수|
|`token.daily-limit`|`0`|일일 토큰 사용 한도(입력+출력 합산). `0` 이면 무제한이며 날짜가 바뀌면 초기화됩니다|
|`ai.debug`|`false`|서버 Debug 로그 출력 여부|

**`ai.api-url` 기본값**

|ai.provider|기본 엔드포인트|
|---|---|
|`openai`|`https://api.openai.com/v1/chat/completions`|
|`claude`|`https://api.anthropic.com/v1/messages`|
|`local`|`http://localhost:11434/v1/chat/completions` (Ollama 기본 포트)|

<br>

## 클라우드 LLM (OpenAI / Claude)

API 키가 필요하며 사용량만큼 과금됩니다.

```properties
ai.provider=openai
ai.api-key=발급받은_API_키
ai.model=gpt-4o-mini
```

> **API 키는 환경변수 `AI_API_KEY` 사용을 권장합니다.**
> 환경변수가 설정되어 있으면 설정 파일보다 우선 적용되므로, 설정 파일에 키를 평문으로 남기지 않아도 됩니다.

## 사내 구축형(로컬) LLM

`Ollama`, `vLLM` 등 **OpenAI 호환 API 를 제공하는 구동 환경**이면 사내 서버의 모델을 연결할 수 있습니다.
구동 환경이 무엇이든 `ai.provider` 값은 항상 `local` 이며, **API 키는 필요하지 않습니다.**
인터넷이 차단된 폐쇄망에서도 사용할 수 있고 LLM API 사용료가 발생하지 않습니다.

```properties
# Ollama - 기본 포트(11434) 를 사용하는 경우
# ai.api-url 은 local 기본값과 동일하므로 생략 가능
ai.provider=local
ai.model=llama3
ai.api-url=http://localhost:11434/v1/chat/completions
```

- vLLM 등 기본 주소가 아닌 환경은 `ai.api-url` 에 해당 주소를 지정합니다.
- 응답이 처리되지 않으면 해당 모델이 JSON 응답 형식을 지원하지 않는 경우이므로 `ai.json-format=false` 로 설정합니다.
- 로컬 LLM 은 모델 로딩과 추론에 시간이 걸릴 수 있으므로 `ai.read-timeout` 을 충분히 크게 잡습니다.

## 이벤트

AI 요청의 전/후 처리는 AISheetSense 전용 범용 이벤트로 제어합니다.
시트 이벤트(`options.Events`)가 아니라 `IBSheet` 객체에 직접 설정하며, 모든 시트에 공통 적용됩니다.

```
사용자 질의 입력
  └→ OnBeforeAI           요청 직전 (파라미터 수정 / 요청 취소 가능)
       └→ 서버 모듈 → LLM Provider
            ├→ 성공 → OnAI
            │          └→ OnBeforeAIApply   시트 적용 직전 (응답 수정 / 적용 취소 가능)
            │               └→ 시트 반영
            └→ 실패 → OnAIError
```

|이벤트|시점|용도|
|---|---|---|
|[OnBeforeAI](/docs/static/on-before-ai)|요청 전송 직전|요청 파라미터 수정, 특정 액션 차단|
|[OnAI](/docs/static/on-ai)|요청 성공|응답 후처리, 사용 이력 로깅|
|[OnBeforeAIApply](/docs/static/on-before-ai-apply)|응답을 시트에 적용하기 직전|응답 검증 / 수정, 위험한 동작 차단|
|[OnAIError](/docs/static/on-ai-error)|요청 실패|오류 유형별 사용자 메시지 처리|

## 트러블슈팅

|증상 / 오류 메시지|원인 및 조치|
|---|---|
|AI 입력창이 표시되지 않음|`AISheetSense` 설정, 플러그인 로드 순서, 서버 모듈 빌드(javax / jakarta), WAS 재시작 여부를 확인합니다|
|`Failed to load ai-gateway.properties`|설정 파일이 `WEB-INF` 바로 아래에 없거나 파일명이 다릅니다. `.sample` 확장자가 남아 있는지 확인합니다|
|`API key is not configured. Check ai-gateway.properties or AI_API_KEY env.`|클라우드 Provider 인데 API 키가 비어 있습니다. `ai.api-key` 또는 환경변수 `AI_API_KEY` 를 확인합니다|
|`AI URL not configured`|요청 경로를 찾지 못했습니다. [AIUrl](/docs/props/cfg/ai-url) 로 경로를 지정합니다|
|`429 insufficient_quota`|LLM Provider 계정의 크레딧이 소진되었습니다. 결제 설정을 확인하고, `cache.enabled` 와 `token.daily-limit` 으로 사용량을 조절합니다|
|로컬 LLM 응답이 시트에 반영되지 않음|모델이 JSON 응답 형식을 지원하지 않는 경우입니다. `ai.json-format=false` 로 설정합니다|
|로컬 LLM 응답이 느리거나 타임아웃됨|최초 요청 시 모델 로딩에 시간이 걸립니다. `ai.read-timeout` 을 크게 설정합니다|
|토큰 사용량 파일이 생성되지 않음|`WEB-INF/feedback` 쓰기 권한을 확인합니다. WAR 을 압축 해제하지 않고 배포하면(`unpackWARs="false"`) 기록이 동작하지 않습니다|

### Read More
- [AISheetSense cfg](/docs/props/cfg/ai-sheetsense)
- [AIUrl cfg](/docs/props/cfg/ai-url)
- [OnBeforeAI static](/docs/static/on-before-ai)
- [OnAI static](/docs/static/on-ai)
- [OnBeforeAIApply static](/docs/static/on-before-ai-apply)
- [OnAIError static](/docs/static/on-ai-error)

### Since

|product|version|desc|
|---|---|---|
|aisheetsense|1.0.0|기능 추가|
