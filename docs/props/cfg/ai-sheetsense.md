# AISheetSense ***(cfg)***

<!-- synonyms: AI, AISheetSense, 자연어, 챗봇, chat, ibsheet-ai-sheetsense.jar, ibsheet-aisheetsense.js, ai-gateway.properties, LLM, GPT, AI 서버모듈, AI 설치, Ollama, vLLM, 로컬 LLM
-->

> IBSheet8 에서 LLM Provider(OpenAI, Anthropic Claude, Ollama, vLLM) 를 활용해 자연어 질의 기능을 이용할 수 있는 챗 다이얼로그를 생성합니다.
> 시트의 데이터 분석/요약/이상치 탐색이나 필터, 그룹핑, 정렬, Formula(수식 적용) 등 시트 기능을 자연어 질문을 통해 확인하고 제어할 수 있습니다.

> `주의` 이 옵션은 **단독으로 동작하지 않습니다.** 서버 모듈(`ibsheet-ai-sheetsense-x.x.x.jar`), 설정 파일(`ai-gateway.properties`),
> 클라이언트 플러그인(`ibsheet-aisheetsense.js`) 이 함께 설치되어 있어야 하며 LLM Provider 의 접속 정보가 필요합니다.<br>
> <mark>설치와 설정 방법은 [AISheetSense 설치 및 설정](/docs/appx/ai-sheetsense-setup) 을 참고하세요.</mark>

![AISheetSense](/assets/imgs/AISheetSense_cfg.png "AI 챗 다이얼로그")



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



### 제약 사항

- OpenAI / Claude 등 클라우드 Provider 는 API 키가 필요합니다. (Provider 측 유료 서비스)
- 응답이 `429 insufficient_quota` 인 경우 Provider 계정의 크레딧 잔액을 확인하세요.
  `OnAIError` 에서 `-429` 로 전달됩니다.
- `CanEdit` 가 `0` 인 보호된 셀은 AI 가 값을 변경할 수 없습니다.
- AI 가 실행하는 시트 API 는 화이트리스트 방식으로 허용된 것만 실행됩니다.
- `ai-gateway.properties` 변경 사항은 WAS 재시작 후 적용됩니다.

### Read More
- [AISheetSense 설치 및 설정 appendix](/docs/appx/ai-sheetsense-setup)
- [AIUrl cfg](./ai-url)
- [OnBeforeAI static](/docs/static/on-before-ai)
- [OnAI static](/docs/static/on-ai)
- [OnBeforeAIApply static](/docs/static/on-before-ai-apply)
- [OnAIError static](/docs/static/on-ai-error)
- [CanEdit col](/docs/props/col/can-edit)

### Since

|product|version|desc|
|---|---|---|
|core|8.4.0.16|기능 추가|
