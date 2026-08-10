# ResultMessage ***(cell)***

<!-- synonyms: ResultMessage, result-message, 결과 메시지, 경고 메시지, DIV 팝업, ResultMask 메시지, 유효성 경고, 팝업 경고문, 검증 실패 메시지, result message, warning popup, validation message, alert message -->

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
sheet.setAttribute(sheet.getRowById("AR99"), "CLS", "ResultMask", "^[\\w\\.\\+%-]+@[A-Za-z0-9\\.-]+\\.[A-Za-z]{2,6}$");
sheet.setAttribute(sheet.getRowById("AR99"), "CLS", "ResultMessage", "이메일 주소를 확인해 주세요.")
sheet.setAttribute(sheet.getRowById("AR99"), "CLS","ResultMessageTime", 800)
```
### Read More
- [ResultText cell](./result-text)
- [ResultMessageTime cell](./result-message-time)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
