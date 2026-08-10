# numberToString ***(static)***

<!-- synonyms: static, 정적 메소드, 전역 함수, static method, global function, IBSheet 정적, numberToString, 숫자 문자열 변환, format number, 숫자 포맷팅 -->

> 숫자를 주어진 포맷에 맞게 마스킹된 문자로 변경하여 리턴합니다

### Syntax
```javascript
string IBSheet.numberToString(num, format);
```

### Parameters
|Name|Type|Required|Description|
|----------|-----|---|----|
|num|`number`|<span class='required'>필수</span>|마스킹 할 숫자|
|format|`string`|<span class='required'>필수</span>|마스킹 적용할 숫자 포맷 ([Format appendix](/docs/appx/format) 참고)|


### Return Value
***string*** : 마스킹이 적용된 문자열

### Example

```javascript
  var maskedNum = IBSheet.numberToString(7314.1654, "#,##0.00");
  //"7,314.17"
```

### Read More
- [stringToNumber static](/docs/static/string-to-number)
- [Format appendix](/docs/appx/format)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
