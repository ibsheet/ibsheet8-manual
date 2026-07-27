# revertCell ***(method)***

<!-- synonyms: 셀 되돌리기, 값 복원, revert cell, 변경 취소 -->

> 특정 셀의 값을 조회된 데이터로 되돌립니다.  
> 데이터의 값과 상태(Added, Changed, Deleted)만 되돌리며, 행/셀/컬럼에 부여된 속성은 그대로 유지됩니다.

### Syntax
```javascript
void revertCell( row, col, render );
```

### Parameters
|Name|Type|Required| Description |
|----------|-----|---|----|
|row |`object`|<span class='required'>필수</span>|[데이터 로우 객체](/docs/appx/row-object)|
|col |`string`|<span class='required'>필수</span>|열이름|
|render |`boolean`|<span class='optional'>선택</span>|즉시 화면 반영 여부<br/>해당 기능을 `0(false)`로 사용했을 경우, 작업 마무리 시에 `rerender()`를 실행해야 화면에 반영 됩니다.<br/>`0(false)`:반영 안함 (`default`)<br/>`1(true)`:즉시 반영|

### Return Value
***boolean*** : 되돌리기 완료 여부

### Example
```javascript
// 특정 셀의 값을 조회된 데이터로 되돌림
sheet.revertCell(sheet.getFirstVisibleRow(), "EMT_DESC", true);
```

### Read More
- [revertRow method](./revert-row)
- [revertData method](./revert-data)
- [Orig cell](/docs/props/cell/orig)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
