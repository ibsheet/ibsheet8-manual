# showCalendar ***(method)***

<!-- synonyms: showCalendar, show-calendar, 달력, 달력 표시, 캘린더, 날짜 선택, 달력 열기, 표시, calendar, open, date, picker -->

> 메소드를 통해 시트 내부에서 달력 컨트롤을 사용하실 수 있습니다. 

### Syntax
```javascript
object showCalendar(row, col, calendar, pos, func, date, always);
```


### Parameters
|Name|Type|Required| Description |
|----------|-----|---|----|
|row |`object`|<span class='required'>필수</span>|[데이터 로우 객체](/docs/appx/row-object)|
|col |`string`|<span class='required'>필수</span>|열이름|
|calendar|`object`|<span class='optional'>선택</span>|캘린더 구성하는 JSON 객체 ([showCalendar](/docs/static/show-calendar)의 `calOption` 참고)
|pos|`object`|<span class='optional'>선택</span>|보여질 달력의 좌우/상하 위치 조정 ex) `{x:10, y:10}`
|func|`function`|<span class='optional'>선택</span>|컨택스트 메뉴에서 사용자가 선택시 `callback` 함수
|date|`string`|<span class='optional'>선택</span>|보여질 달력의 최초 날짜 지정
|always|`boolean`|<span class='optional'>선택</span>|이미 달력이 보여지고 있다면 계속 보여줄지에 대한 여부<br>`0(false)`:달력 보임/감춤에 대한 Toogle (`default`)<br>`1(true)`:달력 보임|


### Return Value
***object*** : 달력 객체


### Example
```javascript
// 현재 포커스가 된 행의 sDate 컬럼에 달력을 생성합니다.
sheet.showCalendar(sheet.getFocusedRow(), "sDate", {Date: "2020-06-02", Format: "yyyy-MM-dd"});
```

### Read More

- [showCalendar static](/docs/static/show-calendar)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.5|기능 추가|
