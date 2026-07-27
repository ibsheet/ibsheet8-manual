# stringToNumber ***(static)***

> 문자열을 지정한 포맷으로 파싱하여 javascript 숫자로 리턴합니다.

### Syntax
```javascript
number IBSheet.stringToNumber(numberStr, format);
```

### Parameters
|Name|Type|Required|Description|
|----------|-----|---|----|
|numberStr|`string`|<span class='required'>필수</span>|숫자 형식의 문자열 (ex:"7,314.1654")|
|format|`string`|<span class='required'>필수</span>|파싱할 포맷|


### Return Value
***number***

### Example
```javascript
  var number = IBSheet.stringToNumber('7,314.1654', "#,##0.00");
  // 7314.1654
```
### Read More
- [numberToString static](/docs/static/number-to-string)
- [Format appendix](/docs/appx/format)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
