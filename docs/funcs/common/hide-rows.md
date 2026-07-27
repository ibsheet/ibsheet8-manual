# hideRows ***(method)***

> 여러 개의 행을 한꺼번에 숨깁니다. 


### Syntax
```javascript
void hideRows( rows );
```

### Parameters

|Name|Type|Required|Description|
|----------|-----|---|----|
|rows|`array[object]`|<span class='optional'>선택</span>|숨길 [데이터 로우 객체](/docs/appx/row-object)의 배열|


### Return Value
***none***


### Example
```javascript
// AR1 행과 AR2행을 한꺼번에 숨깁니다.
sheet.hideRows([sheet.getRowById("AR1"), sheet.getRowById("AR2")]);
```

### Read More

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
