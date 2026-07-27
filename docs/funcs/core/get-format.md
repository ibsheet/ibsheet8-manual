# getFormat ***(method)***

> 특정 셀에 설정된 **Format 값을 확인합니다.**  
> 세 번째 인자 `edit` 값을 `true(1)`로 설정하면 **EditFormat 값**을 확인할 수 있습니다.

### Syntax
```javascript
string getFormat( row, col, edit );
```

### Parameters

|Name|Type|Required| Description |
|----------|-----|---|----|
|row |`object`|<span class='required'>필수</span>|[데이터 로우 객체](/docs/appx/row-object)|
|col |`string`|<span class='required'>필수</span>|열이름|
|edit|`boolean`|<span class='optional'>선택</span>|확인할 포맷 종류 지정<br/>`0(false)`:`Format` 값을 반환 (`default`)<br/>`1(true)`:`EditFormat` 값을 반환|

### Return Value
***string*** : 셀에 설정된 Format 또는 EditFormat 문자열 (설정되지 않은 경우 공백 "" 반환)

### Example
```javascript
//날짜 셀에서 포맷 확인
var f = sheet.getFormat( sheet.getFocusedRow(), "EnterDate" );
var ef = sheet.getFormat( sheet.getFocusedRow(), "EnterDate", 1);

if(f=="yyyy/MM/dd" && ef == "yyyyMMdd"){
    alert("'년/월/일' 순서 포맷입니다. ");
}
```

### Read More
- [getType method](./get-type)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|