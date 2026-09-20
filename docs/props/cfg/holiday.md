# Holiday ***(cfg)***

<!-- synonyms: Holiday, 공휴일, 휴일, 달력 공휴일, 캘린더 휴일, 빨간 날, 휴무일, 공휴일 표시, holiday, holidays, calendar holiday, red day, day off, 특별 날짜, 기념일 -->

> 달력(`Date` 타입 캘린더 팝업)에 **공휴일이나 특정 날짜를 표시**합니다.  
> 지정한 날짜는 캘린더에서 별도의 스타일(빨간 글자 등)로 강조되고, 마우스를 올리면 툴팁(공휴일 이름)이 표시됩니다.  
> 특정 연도의 하루만 지정할 수도 있고, 매년 반복되는 날짜(`*MMDD`), 매월 반복되는 날짜(`**DD`) 등 패턴으로도 지정 가능합니다.

### Type
mixed( `object` \| `array` )

### Options
|Value|Description|
|-----|-----|
|`object`|`{ "날짜키": "공휴일명" }` 또는 `{ "날짜키": { Name, Class } }` 형태의 매핑|
|`array`|`[ { Date: "날짜키", Name, Class }, ... ]` 형태의 배열|

### 날짜 키(Date Key) 형식

|형식|의미|예시|
|---|---|---|
|`YYYYMMDD`|특정 연도·월·일 (8자리)|`"20260101"` — 2026년 1월 1일|
|`*MMDD`|매년 반복 (5자리)|`"*0101"` — 매년 1월 1일|
|`YYYY*DD`|특정 연도의 매월 반복 (7자리)|`"2026*01"` — 2026년 매월 1일|
|`**DD`|매월 반복 (4자리)|`"**01"` — 매월 1일|

### 값(Value) 형식

|필드|Type|Description|
|---|---|---|
|`Name`|`string`|공휴일 이름 (마우스 호버 시 툴팁으로 표시)|
|`Class`|`string`|해당 날짜 셀에 적용할 CSS 클래스명. 미지정 시 기본 공휴일 스타일 적용|

### Example
```javascript
// 1) 간단한 형태 — object로 날짜:이름 매핑
options.Cfg = {
    Holiday: {
        "20260101": "신정",         // 특정 연도 특정 일
        "*0301": "삼일절",           // 매년 3월 1일
        "*0505": "어린이날",         // 매년 5월 5일
        "*1225": "성탄절",
        "**01": "매월 1일"           // 매월 1일 (예: 급여일 표시 용도)
    }
};

// 2) 배열 형태 + Class 지정
options.Cfg = {
    Holiday: [
        { Date: "20260101", Name: "신정",       Class: "MyRedDay" },
        { Date: "20260215", Name: "임시공휴일", Class: "MyGrayDay" },
        { Date: "*0505",    Name: "어린이날" }   // Class 생략 시 기본 공휴일 스타일
    ]
};
```

### Read More
- [MsgLocale cfg](./msg-locale)
- [Type appendix](/docs/appx/type)

### Since

|product|version|desc|
|---|---|---|
|core|8.4.0.19|기능 추가|
