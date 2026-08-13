# Deleted ***(row)***

<!-- synonyms: deleted row, removed row, row deleted state, delete flag, IBColorDeleted, deleteRow flag, 삭제 여부, 삭제된 행, 삭제 상태, 행 삭제, 삭제 표시, Deleted 속성, 삭제 대상, 삭제 행, 삭제 예정 행, 행 삭제 상태, deleted, delete status, deleteRow, 삭제 배경색 -->

> [deleteRow](/docs/funcs/core/delete-row) 함수 호출 시 해당 행의 속성값이 `1(true)`로 설정됩니다.  
> `Deleted`가 `1(true)`이면 삭제 예정 행의 의미로 배경색이 `.IBColorDeleted` 클래스에 정의한 색상으로 변경됩니다.  
> 이 속성은 직접 설정하기보다는 설정값을 확인하는 용도로 사용하실 것을 권합니다.


### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`1(true)`|삭제예정|


### Example
```javascript
//전체 데이터 중에 삭제예정인 행의 개수를 확인
//아래 예제는 Deleted 속성을 확인해보기 위해 작성되었으며,
//실제 삭제예정인 행의 개수를 확인하려면 getRowsByStatus()함수를 사용하시면 됩니다.
var rows = sheet.getDataRows();
var cnt = 0;
for(var i = 0; i < rows.length; i++){
    if (rows[i]["Deleted"]) cnt++;
}
alert(cnt+"개의 삭제예정인 행이 존재합니다.");
```

### Read More
- [Added row](./added)
- [Changed row](./changed)
- [deleteRow method](/docs/funcs/core/delete-row)
- [getRowsByStatus method](/docs/funcs/core/get-rows-by-status)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
