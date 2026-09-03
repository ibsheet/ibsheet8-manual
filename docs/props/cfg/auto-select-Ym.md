# AutoSelectYm ***(cfg)***

<!-- synonyms: AutoSelectYm, auto select year month, calendar year month auto, date picker year month, month year picker, 년월 자동 선택, 연월 선택, 달력 년월, 달력 자동 전환, 월 선택 후 일 선택, 년월 즉시 전환, 달력 확인 버튼, Date 달력 -->

> 기본 `Date` 달력에서 사용자가 년/월 영역을 클릭하여
> 년/월 선택 화면으로 이동했을 때,  
> 월 선택 후 일(日) 선택 달력 화면으로 전환되는 방식을 설정합니다.  
> 기본적으로는 월을 선택한 뒤 확인 버튼을 클릭해야  
> 일 선택 달력이 표시됩니다.  
> `AutoSelectYm` 옵션을 사용하면 확인 버튼 표시 여부와  
> 월 클릭 시 즉시 일 선택 달력으로 전환할지 여부를 제어할 수 있습니다.

### 화면 예시
[`AutoSelectYm: 0 또는 2` 설정 시] <br/>
![AutoSelectYm 0/2 설정 화면](/assets/imgs/autoselectNon.png) <br/>
[`AutoSelectYm: 1` 설정 시] <br/>
![AutoSelectYm 1 설정 화면](/assets/imgs/AutoSelectYm.png) <br/>

### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`0`|확인 버튼 표시<br/>월 선택 후 확인 버튼 클릭 시 일 선택 달력 표시 (`default`)|
|`1`|확인 버튼 미표시<br/>월 클릭 시 즉시 일 선택 달력 표시|
|`2`|확인 버튼 표시<br/>월 클릭 또는 확인 버튼 클릭 모두 일 선택 달력 표시 가능| 

### Example
```javascript
  Cfg : {
    // 확인 버튼 없이 월 클릭 시 바로 일 선택 달력 표시
   "AutoSelectYm": 1
  }
```

### Read More
- [CalendarButtons col](/docs/props/col/calendar-buttons)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.5|기능 추가|
|core|8.0.0.19|`2` 동작 추가|
