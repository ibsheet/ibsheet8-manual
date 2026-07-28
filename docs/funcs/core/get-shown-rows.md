# getShownRows ***(method)***

<!-- synonyms: 보이는 행, 화면 행, 표시된 행, visible rows, shown rows -->

> 보이는 행들의 [데이터 로우 객체](/docs/appx/row-object)를 리턴합니다.  
> 필터링, 트리 접힘 등으로 감춰진 행은 제외됩니다.  
> [getDataRows](./get-data-rows)는 감춰진 행을 포함한 전체 행을, 이 함수는 보이는 행만 리턴합니다.  
> `current:1`(기본값)은 현재 스크롤 위치에서 화면에 보이는 행만, `current:0`은 스크롤 위치와 관계없이 보이는 모든 행을 리턴합니다.

### Syntax
```javascript
array getShownRows(current);
```

### Parameters
|Name|Type|Required| Description |
|----------|-----|---|----|
|current|`boolean`|<span class='optional'>선택</span>|리턴할 영역 설정<br/>`0(false)`:보이는 전체 행<br/>`1(true)`:현재 화면에 보이는 행 (`default`)|

### Return Value
***array[row object]*** : 배열 형태의 [데이터 로우 객체](/docs/appx/row-object)

### Example
```javascript
// 현재 화면에 보이는 행의 개수를 확인
var rowArr = sheet.getShownRows(1);
var cnt = rowArr.length;
```

### Read More
- [getDataRows method](./get-data-rows)
- [getShownCols method](./get-shown-cols)
- [행 객체(Row Object) appendix](/docs/appx/row-object)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.0.0.17|`current` 인자 추가|
