# getPrevShift ***(method)***

<!-- synonyms: getPrevShift, get-prev-shift, 이전 행 탐색, 이전 시프트, 이동, 탐색, previous shift, prev shift, move -->

> [데이터 로우 객체](/docs/appx/row-object)를 대상으로 사용가능한 탐색 메소드입니다.
>
> 기준이 되는 [데이터 로우 객체](/docs/appx/row-object)에서 2번째 인자의 수만큼 이전에 위치한 [데이터 로우 객체](/docs/appx/row-object)를 탐색해서 리턴합니다.


### Syntax
```javascript
object getPrevShift( row, cnt );
```

### Parameters
|Name|Type|Required| Description |
|----------|-----|---|----|
|row|`object`|<span class='required'>필수</span>|검색 기준이 되는 [데이터 로우 객체](/docs/appx/row-object)|
|cnt|`number`|<span class='optional'>선택</span>|기준으로부터 탐색하고자 하는 개수|


### Return Value
***row object*** : [데이터 로우 객체](/docs/appx/row-object)

### Example
```javascript
//AR55행의 7번째 위에 위치한 행을 확인.
var row = sheet.getRowById("AR55");
var nrow = sheet.getPrevShift(row,7);
```

### Read More
- [getNextShift method](./get-next-shift)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
