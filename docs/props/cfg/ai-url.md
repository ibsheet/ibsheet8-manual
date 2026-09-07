# AIUrl ***(cfg)***

<!-- synonyms: AIUrl, AI URL, AI 요청 경로, AI 서버 경로, ai url, api/ai, AISheetSense 경로, AI URL not configured, 서브 디렉토리 컨텍스트 -->

> [AISheetSense](./ai-sheetsense) 챗 다이얼로그가 AI 요청을 전송할 경로를 설정합니다.<br/>
> 서버 모듈 경로를 자동으로 감지하므로 **일반적으로 설정하지 않아도 됩니다.**

### Type
`string`

### 참고

**직접 지정해야 하는 경우**

- AI 서버 모듈을 **별도 서버로 운영**하는 경우
- 애플리케이션이 **서브 디렉토리 컨텍스트**로 배포된 경우

경로가 잘못 지정되면 [OnAIError](/docs/static/on-ai-error) 에 `"AI URL not configured"` 가 전달됩니다.

### Example

**서브 디렉토리 컨텍스트로 배포된 경우**
```javascript
options.Cfg = {
    AISheetSense: 1,
    AIUrl: '/myapp/api/ai'      // /myapp 컨텍스트에 배포된 경우
};
```

**AI 서버 모듈을 별도 서버로 운영하는 경우**
```javascript
options.Cfg = {
    AISheetSense: 1,
    AIUrl: 'https://ai.example.com/api/ai'
};
```

### Read More
- [AISheetSense cfg](./ai-sheetsense)
- [Export.Url cfg](./export)
- [OnAIError static](/docs/static/on-ai-error)

### Since

|product|version|desc|
|---|---|---|
|core|8.4.0.16|기능 추가|
