# setValue ***(method)***
> 셀의 값을 지정한 값으로 변경합니다.   
> 기본적으로 이 함수를 호출해도 편집 관련 이벤트(`onAfterChange`, `onEndEdit` 등)는 발생하지 않습니다.  
> 단, 데이터가 편집 상태일 때 `setValue`를 호출하면 `onEndEdit` 이벤트가 발생합니다.   
> 이 경우 `ignoreEvent`옵션을 사용하여 이벤트 발생을 방지할 수 있습니다.  
> 값 변경 시 `Change` 이벤트 처리가 필요한 경우 [OnChange](/docs/props/event/on-change) 이벤트를 사용해야 합니다.

### Syntax
```javascript
boolean setValue( row, col, val, render, ignoreEvent, noCalc );
```

### Parameters
|Name|Type|Required| Description |
|----------|-----|---|----|
|row|`object`|<span class='required'>필수</span>|[데이터 로우 객체](/docs/appx/row-object)|
|col|`string`|<span class='required'>필수</span>|열이름|
|val|`number` \| `string`|<span class='required'>필수</span>|입력값(셀 타입에 맞는 값)|
|render|`boolean`|<span class='optional'>선택</span>|값 변경 시 즉시 화면에 반영할지 여부입니다. <br/>`false(0)`로 설정할 경우 화면에 즉시 반영되지 않으며, 작업 완료 후 `rerender()` 또는 상황에 따라 `refreshCell`, `refreshRow`, `renderBody` 등의 렌더링 함수를 호출해야 합니다.<br/>`true(1)`: 즉시 반영 (`default`)|
|ignoreEvent|`object` \| `boolean`|<span class='optional'>선택</span>|`setValue` 호출 시 발생하는 이벤트를 제어하는 옵션입니다. <br/>객체 형태로 설정할 수 있으며, 이벤트 이름을 key로 지정하고 `true`로 설정하면 해당 이벤트는 발생하지 않습니다. <br/>`true / false`로 설정할 경우 `onEndEdit` 이벤트만 제어합니다.|
|calc|`boolean`|<span class='optional'>선택</span>|포뮬러 계산 여부 <br/> 해당 기능을 `0(false)`로 설정할 경우 `setValue`시 포뮬러 계산이 이뤄지지 않습니다.  <br/>포뮬러를 반영하려면 이후 반드시 `calculate()`를 호출해줘야 됩니다.(`default:1`) |

### ignoreEvent Options

| Name | Type | Required | Description |
|------|------|----------|-------------|
| OnChange| `boolean` | <span class="optional">선택</span> | `setValue`시 발생하는 `OnChange` 이벤트 발생 여부를 제어합니다.<br/> true 리턴시 해당 이벤트가 발생하지 않습니다. (`default: 0(false)`) |
| OnSame| `boolean` | <span class="optional">선택</span> | `setValue`시 발생하는 `OnSame` 이벤트 발생 여부를 제어합니다.<br/> true 리턴시 해당 이벤트가 발생하지 않습니다. (`default: 0(false)`) |
|onEndEdit| `boolean` | <span class="optional">선택</span> | 편집상태에서 `setValue`를 할 경우, 기본적으로 `onEndEdit` 이벤트가 발생합니다. <br/> 이때 발생하는 `onEndEdit` 이벤트의 발생 여부를 제어합니다. <br> true를 리턴할 경우, 해당 이벤트가 발생하지 않습니다. (`default: 0(false)`)|

<!-- ### ignoreEvent를 true/false로 설정할 경우 
`ignoreEvent`를 true/false로 설정할 경우, 기존의 5번째 인자 옵션인 `ignoreOnEndEdit`으로 동작합니다. <br>`ignoreOnEndEdit`은 기본적으로 `ignoreEvent`의 `onEndEdit` 인자와 동일하게 동작하며 true를 설정할 경우 `onEndEdit` 이벤트가 발생하지 않게 동작합니다. <br> 다만 해당 옵션은 deprecated되었으니 `ignoreEvent` 사용을 권장하는 바입니다. -->

### Return Value
***boolean*** : 값의 변경 여부 (값이 변경되면 `1(true)`, 변경되지 않으면(기존값과 동일한 경우) `0(false)`)

### Example
```javascript
// ================================
// 데이터행 변경 예제
// ================================

// 5번째 행 가져오기 (row 객체의 id가 AR5이다.)
var r5 = sheet.getRowById("AR5");

// AR5 데이터 행의 StartDate, EndDate 값을 변경
sheet.setValue( r5, "StartDate", "20160105");
sheet.setValue({row:r5, col:"EndDate", val:"20160315"});

//OnChange, onEndEdit 발생시키지 않음
sheet.setValue({row:r5, col:"A", val:10, ignoreEvent:{onEndEdit:true,OnChange:true}});

// ================================
// 데이터행 변경 예제
// 여러 행 반복 처리 (calc:0, render:0으로 매번 계산·렌더링 생략 — 성능 최적화)
// ================================

var Rows = sheet.getDataRows(); //시트의 모든 데이터 행 추출

for(var i=0; i<Rows.length; i++){
    //마감열(Name:close_data) 컬럼 값 일괄 변경
    sheet.setValue({row:Rows[i], col:"close_data", val:"변경", calc:0, render:0});
}
// 마지막에 Formula 한 번만 계산 + 화면 일괄 반영
sheet.calculate(false, false);
sheet.rerender(1);

// ================================
//헤더행 변경 예제
// ================================

var hr = sheet.getRowById("Header"); // 최상단 헤더 행 가져오기

// 특정 컬럼 헤더 텍스트 변경
sheet.setValue(hr, "SalesToday", "매출");
sheet.setValue(hr, "SalesSum", "매출");  
sheet.setValue(hr, "CostToday", "비용");
sheet.setValue(hr, "CostSum", "비용"); 

// 헤더 텍스트 변경 후 경우에 따라 Merge 재적용(행 기준 병합)
sheet.setAutoMerge( {headerMerge:2});

// ================================
//합계행 변경 예제
// ================================

//(Col) FormulaRow 설정한 합계 컬럼은 자동 계산되므로 setValue로 직접 변경할 수 없습니다.
var sumRow = sheet.getRowById("FormulaRow"); // 합계행 가져오기

//(Col) FormulaRow가 적용되지 않은 컬럼은 변경 가능
sheet.setValue(sumRow , "Notes", "합계 참조용 메모");

```

### Read More
- [getDataRows method](./get-data-rows)
- [getRowById method](./get-row-by-id)
- [getValue method](./get-value)
- [getString method](./get-string)
- [setString method](./set-string)
- [setAutoMerge method](./set-auto-merge)
- [setRowValue method](./set-row-value)
- [calculate method](./calculate)
- [recalculate method](./recalculate)
- [recalculateRows method](./recalculate-rows)
- [rerender method](./rerender)
- [refreshCell method](./refresh-cell)
- [refreshRow method](./refresh-row)
- [renderBody method](./render-body)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.0.0.11|`ignoreOnEndEdit` 추가|
|core|8.2.0.21|`ignoreEvent` 추가, `ignoreOnEndEdit` deprecated 처리|
|core|8.3.0.45|`calc` 추가|