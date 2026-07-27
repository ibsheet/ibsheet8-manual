# setMessage ***(method)***
> 시트에 새로운 메시지를 설정합니다.
> 결과로 받은 객체를 통해 메시지의 설정/변경사항을 확인할 수 있습니다.

### Syntax
```javascript
object setMessage( key, type, message );
```

### Parameters
|Name|Type|Required|Description|
|----------|-----|---|----|
|key|`string`|<span class='required'>필수</span>|메시지 이름|
|type|`string`|<span class='required'>필수</span>|메시지 종류<br>`'Alert'`, `'Text'`(`default`) 중 선택|
|message|`string`|<span class='required'>필수</span>|메시지 내용|


### Return Value
***object***

### Example
```javascript
// 시트에 메시지를 설정합니다.
var result = sheet.setMessage("Warning", "Text", "잘못된 값입니다.");
```

### Read More
- [getMessage method](./get-message)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
