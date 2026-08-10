# hideMessage ***(method)***

<!-- synonyms: hideMessage, hide-message, 메시지 감춤, 메시지 숨김, 메시지 제거, 다이얼로그 닫기, 메시지 닫기, hide, message, dialog, close -->

> [showMessage](./show-message)로 띄운 메세지 다이얼로그를 제거합니다.

###
![hideMessage](/assets/imgs/showMessage.png "시트 영역 위에 메세지 다이얼로그를 띄움")

### Syntax
```javascript
void hideMessage();
```

### Return Value
***none***

### Example
```javascript
function popup(){
    sheet.showMessage({message:"<span style='color:black'>결제기한이 만료되었습니다.</span>",importance:4,type:1});
    setTimeout(function(){sheet.hideMessage()} , 1000);
}
```

### Read More
- [showMessage method](./show-message)
- [onHideMessage event](/docs/events/on-hide-message)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
