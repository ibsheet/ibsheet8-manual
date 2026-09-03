# CalendarButtons ***(col)***

<!-- synonyms: 달력 버튼, 달력 하단 버튼, 오늘 버튼, 어제 버튼, 확인 버튼, 취소 버튼, 이번달 버튼, calendar button, 날짜 선택 버튼 -->

> 달력이 표시될 때 달력 하단에 보여질 버튼을 설정합니다.  
> 설정값의 합을 통해 여러 개 버튼을 표시할 수도 있습니다.  
> 년/월 달력에서 월 선택 후 일(日) 달력으로 넘어가려면 기본적으로 `확인` 버튼(값 `4`)이 필요합니다.  
> `확인` 버튼을 넣지 않으려면 [AutoSelectYm](/docs/props/cfg/auto-select-Ym)을 `1`로 설정하세요. 월 클릭 시 바로 일 달력으로 전환됩니다.

### 화면 예시

1. 년월일 달력

![CalendarButtons](/assets/imgs/calendarButtons.png "CalendarButtons")

2. 년월 달력

![MonthCalendarButtons](/assets/imgs/monthCalendar.png "MonthCalendarButtons")


### Type
`number`

### Options

> CalendarButtons를 설정하면 `년월일`, `년월`, `년` 달력 **모두**에 그 값이 적용되며(각 모드는 아래 표 참고), 설정하지 않으면 각 모드의 `default`가 사용됩니다.

* 년월일 달력 (`default: 0`)

|Value|Description|
|-----|-----|
|`1`|"오늘" 버튼|
|`2`|"전체취소" 버튼|
|`4`|"확인" 버튼|
|`8`|"어제" 버튼|

* 년월 달력  (`default: 4`)

|Value|Description|
|-----|-----|
|`1`|"이번달" 버튼|
|`2`|"전체취소" 버튼|
|`4`|"확인" 버튼|

* 년 달력  (`default: 4`)

|Value|Description|
|-----|-----|
|`2`|"전체취소" 버튼|
|`4`|"확인" 버튼|

### Example
```javascript
options.Cols = [
    ...
    // 년월일 달력에 어제, 오늘 버튼을 표시한다.
    {Type: "Date", Name: "sa_enterDate", CalendarButtons: 9 ...},
    ...
    // 년월 달력에 이번달, 전체취소, 확인 버튼을 표시한다.
    {Type: "Date", Name: "sa_monthDate", CalendarButtons: 7, Format: "yyyy/MM" ...}
];
```

### Read More

- [AutoSelectYm cfg](/docs/props/cfg/auto-select-Ym)
- [AutoCalendar cfg](/docs/props/cfg/auto-calendar)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
