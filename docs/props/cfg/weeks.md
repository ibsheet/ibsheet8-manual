# Weeks ***(cfg)***

<!-- synonyms: Weeks, week number, calendar weeks, week of year, 주차, 주차 표현, 달력 주차, 주 번호, 달력 주 표시, 몇 주차 -->

> 달력의 주차 표현 여부를 설정합니다.
>
> 사용자가 직접 [showCalendar](/docs/static/show-calendar)를 호출하는 경우엔 적용되지 않습니다. (직접 호출하는 경우 메소드 인자에 따로 설정해야합니다).

### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`0`|주차 표현 안함 (`default`)<br> !["기본값"](/assets/imgs/weeks_0.png "기본값")|
|`1`|주차 표현<br> !["주차 표현"](/assets/imgs/weeks_1.png  "주차 표현")|


### Example
```javascript
options.Cfg = {
   "Weeks": 1   // 주차 표현
};
```

### Read More
- [showCalendar static](/docs/static/show-calendar)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
