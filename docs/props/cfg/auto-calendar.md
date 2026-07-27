# AutoCalendar ***(cfg)***
> [Type](/docs/appx/type)이 `Date`인 컬럼에서, 사용자가 셀 편집 모드로 들어갈 때 달력을 자동으로 표시할지 여부를 설정합니다.   
> (편집 모드 진입: Enter, 더블 클릭, 키 입력, F2 등)

<!-- synonyms: auto calendar, date picker auto open, open calendar automatically, edit open calendar, date calendar popup, 자동 달력, 달력 자동 열기, 편집 시 달력 표시, Date 타입 달력, 달력 아이콘 없이 자동 -->


### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0`(`false`)|기능 사용 안함 (`default`)<br/>- 달력 아이콘 표시 <br/>- 아이콘 클릭 시 달력 표시|
|`1`(`true`)|편집 모드 진입 시 달력 자동 표시<br/>- 달력 아이콘은 표시되지 않음|


### Example
```javascript
// Date 타입 열 편집 시 달력을 자동으로 오픈
options.Cfg = {
    AutoCalendar: true
};
```

### Read More


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
