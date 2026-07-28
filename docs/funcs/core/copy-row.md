# copyRow ***(method)***

<!-- synonyms: 행 복사, 로우 복사, 단일 행 복사, copy row, 행 복제 -->

> 지정한 행을 특정 위치로 복사합니다.  
> 값뿐 아니라 셀 속성(색상, 글자색 등)도 함께 복사됩니다. (`empty: true`로 호출하면 데이터를 복사하지 않고 행만 추가됩니다.)  
> 행이 추가되므로 [onRowAdd](/docs/events/on-row-add) 이벤트가, 복사 동작이므로 [onAfterRowCopy](/docs/events/on-after-row-copy) 이벤트가 발생합니다.

### Syntax
```javascript
object copyRow( row , next , empty , parent , child, forceVisible );
```

### Parameters
|Name|Type|Required|Description|
|----------|-----|---|----|
|row|`object`|<span class='required'>필수</span>|[데이터 로우 객체](/docs/appx/row-object)|
|next|`object`|<span class='optional'>선택</span>|[데이터 로우 객체](/docs/appx/row-object)<br/>(next로 지정한 행의 위에 row행이 복사됨. 값이 없으면 맨 마지막행에 복사)|
|empty|`boolean`|<span class='optional'>선택</span>|복사 시 데이터 포함 여부<br>`1(true)`로 설정하여 사용 시 [onAfterRowCopy](/docs/events/on-after-row-copy) 이벤트 미발생<br/>`0(false)`:데이터 포함 (`default`)<br/>`1(true)`:데이터 미포함|
|parent|`object`|<span class='optional'>선택</span>|[데이터 로우 객체](/docs/appx/row-object) (트리 사용시 부모에 해당하는 행 지정)|
|child|`boolean`|<span class='optional'>선택</span>|트리 사용시 자식행도 복사할 지 여부<br/>`0(false)`:자식행 미포함 (`default`)<br/>`1(true)`:자식행 포함|
|forceVisible|`boolean`|<span class='optional'>선택</span>|보이지 않는 행을 복사할 때 보이도록 설정<br/>`0(false)`:행을 감춤(Visible:`0(false)`) 상태로 변경 시키고 복사 (`default`)<br/>`1(true)`:행을 보임(Visible:`1(true)`) 상태로 변경 시키고 복사|

### Return Value
***object*** : 복사된 [데이터 로우 객체](/docs/appx/row-object)

### Example
```javascript
//AR5 행을 포커스 행 위로 복사
var row = sheet.copyRow({row:sheet.getRowById("AR5"), next:sheet.getFocusedRow()});

//AR5 행을 포커스 행 아래로 복사
var row = sheet.copyRow({row:sheet.getRowById("AR5"), "next":sheet.getNextRow(sheet.getFocusedRow())});

//복사한 행을 감춘다.
row["Visible"] = 0;
sheet.renderBody();
```

### Read More
- [addRow method](./add-row)
- [moveRow method](./move-row)
- [onRowAdd event](../../events/on-row-add)
- [onAfterRowCopy event](../../events/on-after-row-copy)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|