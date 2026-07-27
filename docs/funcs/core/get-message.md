# getMessage ***(method)***
> 시트에서 메시지를 가져옵니다.

### Syntax
```javascript
string getMessage( key, type );
```

### Parameters
|Name|Type|Required|Description|
|----------|-----|---|----|
|key|`string`|<span class='required'>필수</span>|메시지 이름|
|type|`string`|<span class='optional'>선택</span>|가져올 메시지 종류<br>`'Alert'`, `'Text'(default)` 중 선택|


### Return Value
***String***

### Example
```javascript
// msg 파일의 Alert 밑에 있는 CanCancelChanges 메시지 내용을 가져옵니다.
var message1 = sheet.getMessage("CanCancelChanges", "Alert");

// msg 파일의 Text 밑에 있는 CanCancelChanges 메시지 내용을 가져옵니다.
var message2 = sheet.getMessage("Render");
```

### Read More
- [setMessage method](./set-message)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
