# getBodyWidth ***(method)***

> 특정 [Section](/docs/props/col/section)의 너비(틀고정 기준 좌/우측)를 확인합니다.

### Syntax
```javascript
number getBodyWidth( section );
```

### Parameters

|Name|Type|Required|Description|
|----------|-----|---|----|
|section |`number`|<span class='optional'>선택</span>|너비를 알고 싶은 영역<br>`0`:왼쪽<br>`1`:가운데 (`default`)<br>`2`:오른쪽|

### Return Value
***number*** : 섹션의 너비 (pixel 단위)

### Example
```javascript
//왼쪽 틀고정 영역의 너비를 확인
var w = sheet.getBodyWidth(0);
```

### Read More
- [getBodyHeight method](./get-body-height)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
