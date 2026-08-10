# stringToDate ***(static)***

<!-- synonyms: static, 정적 메소드, 전역 함수, static method, global function, IBSheet 정적, stringToDate, 문자열 날짜 변환, parse date, 날짜 파싱 -->

> 문자열을 지정한 포맷으로 파싱하여 javascript `Date객체`로 리턴합니다.

### Syntax
```javascript
object IBSheet.stringToDate(dateStr, format);
```

### Parameters
|Name|Type|Required|Description|
|----------|-----|---|----|
|dateStr|`string`|<span class='required'>필수</span>|날짜 형식의 문자열 (ex:"2018-02-23" or "30/04/2015"|
|format|`string`|<span class='required'>필수</span>|파싱할 포맷|


### Return Value
***object*** : javascript Date 객체

### Example
```javascript
  var dateObj = IBSheet.stringToDate("20180226", "yyyyMMdd");
  //Mon Feb 26 2018 00:00:00 GMT+0900 (한국 표준시)

  var dateObj = IBSheet.stringToDate("15-05-2019", "dd-MM-yyyy");
  //Wed May 15 2019 00:00:00 GMT+0900 (한국 표준시)
```
### Read More
- [dateToString static](/docs/static/date-to-string)
- [Format appendix](/docs/appx/format)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
