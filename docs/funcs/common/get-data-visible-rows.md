# getDataVisibleRows ***(method)***

<!-- synonyms: get data visible rows, visible data rows, currently visible rows, filtered visible rows, get shown rows, visible row objects, 보이는 데이터 행, 보이는 행 조회, 표시된 행 가져오기, 화면 보이는 로우, 필터 후 보이는 행, getDataVisibleRows 메소드 -->

> 시트에서 보여지고 있는 데이터 로우 객체들을 확인합니다. 

### Syntax
```javascript
void getDataVisibleRows( noSubTotal );
```

### Parameters

|Name|Type|Required|Description|
|----------|-----|---|----|
|noSubTotal|`boolean`|<span class='optional'>선택</span>|소계/누계 행을 제외할지 여부|

### Return Value
***none***

### Return Value
***array[row object]*** : 데이터 로우 객체 배열


### Example
```javascript
// 시트에서 보여지고 있는 데이터 로우 객체들을 반환합니다.
sheet.getDataVisibleRows();
```

### Read More

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
