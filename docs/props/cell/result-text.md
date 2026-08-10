# ResultText ***(cell)***

<!-- synonyms: ResultText, result-text, 결과 알림, alert 메시지, 경고문 텍스트, ResultMask 알림, 유효성 알림, 검증 실패 문구, alert 문구, result text, alert text, validation alert, warning text -->

> [ResultMask](./result-mask)에 위배되는 내용이 입력시 alert으로 보여줄 내용을 설정합니다.

### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`string`|잘못된 내용이 입력시 보여질 경고문 내용|

### Example
```javascript
//특정 셀에서 ResultMask 속성 위배시 메세지 설정
var ROW = sheet.getRowById("AR10");
ROW["CLSResultText"] = "숫자만 입력 가능합니다.";
//변경내용 확인
sheet.refreshCell({row:ROW, col:"CLS"});
```

### Read More
- [ResultMask cell](./result-mask)
- [ResultMessage cell](./result-message)
- [EditMask cell](./edit-mask)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
