# getDataRows ***(method)***

<!-- synonyms: 전체 행, 전체 데이터, 데이터 행, 로우 배열, all rows -->

> 시트가 가지고 있는 전체 데이터 행을 리턴합니다.

### getDataRows 함수로 Row 객체 접근시 주의사항
- Text 컬럼(`Type:"Text"`)에 숫자 데이터를 조회하면 → **Row 객체에는 숫자형 값이 들어 있음**
  - 문자 형태로 사용하려면 [OrigSearchData](/docs/props/col/orig-search-data)를 설정하거나 [getValue](./get-value) 함수를 이용
- Date 컬럼(Type: "Date")에서 `DataFormat`에 맞는 데이터를 조회해도  → **Row 객체에 숫자형(timestamp) 값이 들어 있음**
   - `DataFormat`에 맞는(ex : 20260101) 형태로 사용하려면 [getValue](./get-value) 또는 [dateToString](/docs/static/date-to-string) 사용
- Row 객체에 직접 접근하여 값을 변경해도 → `행 상태(Changed)에는 영향을 주지 않음`

> 빈 값(`Int`/`Float`의 `""`/`null`) 처리 등 직접 접근 상세는 [행 객체](/docs/appx/row-object)를 참고하세요.

<!--! [비공개] SearchMode:5 기능 추가로 인한 비공개 처리
> 일반조회의 경우 조회한 모든 데이터 행을 리턴하며, 서버 스크롤 조회([SearchMode](/docs/props/cfg/search-mode):3)의 경우 해당 페이지까지 조회해온 데이터 행을 리턴 합니다. 
>
> 만약 서버페이징([SearchMode](/docs/props/cfg/search-mode):4)의 경우 조회한 페이지 데이터만 리턴 합니다.  <br/>1,3,5 페이지를 조회 했을 경우 1,3,5 페이지의 데이터를 리턴 합니다. 
[AlwaysSearchPage](/docs/props/cfg/always-search-page):1 로 설정한 경우 currentPage 인자를 1로 설정하면 현재 보여지고 있는 페이지의 데이터만 리턴 합니다.<br/>
!-->

### Syntax
```javascript
array getDataRows( noSubTotal);
```

### Parameters

|Name|Type|Required|Description|
|----------|-----|---|----|
|noSubTotal |`boolean`|<span class='optional'>선택</span>|소계/누계 행을 제외할지 여부<br>`0(false)`:소계/누계 행 포함 (`default`)<br>`1(true)`:소계/누계 행 제외|
<!--![비공개] SearchMode:5 기능 추가로 인한 비공개 처리
|currentPage |`boolean`|<span class='optional'>선택</span>|현재 보여지는 페이지 데이터 반환 여부<br>`0(false)`:전체 페이지 데이터 반환 (`default`)<br>`1(true)`:현재 보여지는 페이지 데이터 반환|
!-->

### Return Value
***array[row object]*** : [데이터 로우 객체](/docs/appx/row-object)를 담고있는 배열

### Example
```javascript
// 전체 데이터행을 가져온다.
var Rows = sheet.getDataRows();

for(var i=0; i<Rows.length; i++){
    // 마감열(saveName:close_data)에 값을 일괄변경하는 경우, render속성을 꺼야 속도가 빠르다.
    sheet.setValue({row:Rows[i], col:"close_data", val:"변경", render:0});
    //Rows[i].close_data = "변경"; row 객체에 직접 값을 변경하면 행 상태(Changed)가 변경되지 않아 저장 대상에서 제외됩니다.
}
//변경사항 적용한다.
sheet.rerender(1);

// 보이는 행의 합계, 평균, 최대값, 최소값 구하기
var col = "IntData";
// row.Visible — 0:감춤, 1:보임
var visibleRows = sheet.getDataRows().filter(function(row){ return row.Visible; });

var sum = visibleRows.reduce(function(a, c){ return a + c[col]; }, 0);
var avg = sum / visibleRows.length;
var max = visibleRows.reduce(function(a, c){ return Math.max(a, c[col]); }, -Infinity);
var min = visibleRows.reduce(function(a, c){ return Math.min(a, c[col]); }, Infinity);
```

### Read More
- [행 객체](/docs/appx/row-object)
- [getTotalRowCount method](./get-total-row-count)
- [OrigSearchData col](/docs/props/col/orig-search-data)
- [getShownRows method](./get-shown-rows)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.0.0.4|`noSubTotal` 인자 추가로 소계/누계 행을 제외한 데이터 행만 가져오는 기능 추가|
<!--![비공개] SearchMode:5 기능 추가로 인한 비공개 처리
|core|8.1.0.23|`currentPage` 인자 추가로 현재 보여지는 페이지의 데이터 행만 가져오는 기능 추가|
!-->
