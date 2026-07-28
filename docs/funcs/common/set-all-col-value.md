# setAllColValue ***(method)***

> setValue를 이용하여 하나 컬럼의 전체 데이터행 값을 일괄적으로 변경합니다. 

### Syntax
```javascript
void setAllColValue( colName, value );
```

### Parameters

|Name|Type|Required|Description|
|----------|-----|---|----|
|colName|`string`|<span class='optional'>선택</span>|열 이름|
|value|`string`|<span class='optional'>선택</span>|입력값|

### Return Value
***none***

### Example
```javascript
// StartDate 컬럼의 값을 20210124로 일괄 변경합니다.
sheet.setAllColValue("StartDate", "20210124");
```

### Read More

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
