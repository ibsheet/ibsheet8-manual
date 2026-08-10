# removeHTMLTag ***(static)***

<!-- synonyms: static, 정적 메소드, 전역 함수, static method, global function, IBSheet 정적, removeHtmlTag, HTML 제거, 태그 제거, strip html -->

> 인자로 들어온 문자열에서 HTML Tag형식의 문자열을 제거해서 문자열을 리턴합니다.

### Syntax
```javascript
string IBSheet.removeHTMLTag(html);
```

### Parameters
|Name|Type|Required|Description|
|----------|-----|---|----|
|html|`string`|<span class='required'>필수</span>|대상 문자열|


### Return Value
***string*** : HTML Tag가 제거된 문자열

### Example
```javascript
  var string = IBSheet.removeHTMLTag("<div><p>안녕하세요.<br/><span style='font-family: consolas;'>Hello, World~!</span></p></div>");
  // "안녕하세요.Hello, World~!"
```
### Read More

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
