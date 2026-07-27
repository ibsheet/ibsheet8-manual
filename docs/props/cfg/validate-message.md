# ValidateMessage ***(cfg)***

<!-- synonyms: 검증 메시지, 유효성 메시지, validate message, 검증 실패 메시지 -->

> [ValidCheck](./valid-check) 활성화 시 검증 실패에 대해 추가로 표시할 통일된 메시지를 설정합니다.  
> 어떤 검사가 실패했는지와 무관하게 동일 메시지가 표시됩니다.  
> 마킹된 셀의 호버 툴팁(메시지 파일에 정의된 `RequiredError`, `SizeError`, `EditMaskError`, `ResultMaskError` 키 값)과는 **별도로 함께** 표시됩니다.  
> 미설정 시 추가 메시지는 표시되지 않습니다 (마킹 + 호버 툴팁만 동작).

### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`string`|검사 실패 시 표시할 메시지 문자열|

### Example
```javascript
options.Cfg = {
    ValidCheck: true,
    ValidateMessage: "입력값을 확인해주세요."
};
```

### Read More
- [ValidCheck cfg](./valid-check)
- [doSave method](/docs/funcs/core/do-save)
- [getSaveJson method](/docs/funcs/core/get-save-json)
- [getSaveString method](/docs/funcs/core/get-save-string)

### Since

|product|version|desc|
|---|---|---|
|core|8.2.0.3|기능 추가|