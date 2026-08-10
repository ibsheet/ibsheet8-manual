# ResultMessage ***(col)***

<!-- synonyms: 검증 실패 메시지, 오류 메시지, 팝업 경고, ResultMask 메시지, result message, validation message, error popup, warning text -->

> [ResultMask](./result-mask)에 위배되는 내용이 입력시 DIV 레이어 팝업으로 보여질 내용을 설정합니다.


### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`string`|잘못된 내용이 입력시 보여질 경고문 내용|

### Example
```javascript
//이메일 주소 확인
options.Cols = [
    ...
    {Type: "Text",
        ResultMask: "^[\\w\\.\\+%-]+@[A-Za-z0-9\\.-]+\\.[A-Za-z]{2,6}$",
        ResultMessage: "이메일 주소를 확인해 주세요.",
        ResultMessageTime: 800,
        Name:"sa_email", Width: 120 ...},
    ...
];
```
### Read More
- [ResultText col](./result-text)
- [ResultMessageTime col](./result-message-time)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
