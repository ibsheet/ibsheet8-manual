# revertRow ***(method)***

<!-- synonyms: 행 되돌리기, 값 복원, revert row, 변경 취소 -->

> 특정 행의 모든 셀 값을 조회된 데이터로 되돌립니다.  
> 데이터의 값과 상태(Added, Changed, Deleted)만 되돌리며, 행/셀/컬럼에 부여된 속성은 그대로 유지됩니다.

### Syntax
```javascript
void revertRow( row, render );
```

### Parameters

|Name|Type|Required| Description |
|----------|-----|---|----|
|row |`object`|<span class='required'>필수</span>|[데이터 로우 객체](/docs/appx/row-object)|
|render |`boolean`|<span class='optional'>선택</span>|즉시 화면 반영 여부<br/>해당 기능을 `0(false)`로 사용했을 경우, 작업 마무리 시에 `rerender()`를 실행해야 화면에 반영 됩니다.<br/>`0(false)`:반영 안함 (`default`)<br/>`1(true)`:즉시 반영|

### Return Value
***boolean*** : 되돌리기 완료 여부

### Example
```javascript
// 포커스된 행의 모든 셀 값을 조회된 데이터로 되돌림
sheet.revertRow(sheet.getFocusedRow(), true);
```

### Read More
- [revertCell method](./revert-cell)
- [revertData method](./revert-data)
- [Orig cell](/docs/props/cell/orig)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
