# getRowTop ***(method)***

<!-- synonyms: getRowTop, get-row-top, 행 y좌표, 로우 y좌표, 행 위치, 위치 확인, 좌표 조회, position, top, y-coordinate -->

> 데이터 행 내에서 y좌표값을  확인합니다.
>
> 최상단 행은 `0`을 리턴합니다.

### Syntax
```javascript
number getRowTop( row );
```

### Parameters

|Name|Type|Required| Description |
|----------|-----|---|----|
|row |`object`|<span class='required'>필수</span>|[데이터 로우 객체](/docs/appx/row-object)|

### Return Value
***number*** : 데이터 영역 최상단을 기준으로 행의 y좌표 (pixel 단위)

### Example
```javascript
//선택행의 RowTop 값을 가져온다.
var w = sheet.getRowTop( sheet.getFocusedRow() );
```

### Read More
- [getBodyHeight method](./get-body-height)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
