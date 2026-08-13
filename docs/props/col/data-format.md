# DataFormat ***(col)***

<!-- synonyms: 날짜 데이터 형식, 서버 날짜 포맷, yyyyMMdd, 조회 날짜 형식, 저장 날짜 형식, 원본 날짜 포맷, data format, date format server, raw date, save date format, parse stringify, 커스텀 날짜 포맷, 커스텀 파서, custom date format -->

> `Date` 타입 컬럼에서 **서버에서 조회되는 날짜 데이터의 형식(format)** 을 지정합니다.  
> 예를 들어 조회 데이터가 `"25012017"` (25일 01월 2017년)이라면 `DataFormat: "ddMMyyyy"`로,  
> 조회 데이터가 `"20171225"` (2017년 12월 25일)라면 `DataFormat: "yyyyMMdd"`로 설정해야 합니다.  
> 해당 열의 데이터가 서버로 저장될 때 ([doSave](/docs/funcs/core/do-save), [getSaveString](/docs/funcs/core/get-save-string)) 지정된 `DataFormat` 형식으로 변환되어 전송됩니다.  
>
> `DataFormat`이 설정되지 않은 경우 날짜 데이터는 **표시 형식과 값 추출 형식이 서로 다르게 처리됩니다.**  
> 예를 들어 `getValue`는 `timestamp` 값으로 반환되며,  
> 저장 시에는 **Format이 적용된 화면 표시 값** 기준으로 처리됩니다.
>
> 문자열 포맷으로 표현할 수 없는 특수한 날짜 형식(예: ISO 8601, RFC, epoch 초 단위, 회사 내부 규격 등)은 **object 형식**(`{parse, stringify}`)으로 지정해 파싱·직렬화 로직을 직접 구현할 수 있습니다.

### 날짜 예약어

|표시|의미|
|---|---|
|`yyyy`|년도(4자리)|
|`MM`|월(2자리)|
|`dd`|일(2자리)|
|`HH`|시간(2자리)|
|`mm`|분(2자리)|
|`ss`|초(2자리)|
|`fff`|밀리초(3자리)|
|`z`|타임존 오프셋 (포맷 끝, 파싱 시 UTC 보정)|

전체 예약어와 세부 사용법은 [Format appendix](/docs/appx/format#date-format)를 참고하세요.

### Type
mixed( `string` \| `object` )

### Options
|Value|Description|
|-----|-----|
|`string`|`yyyyMMdd` 등 날짜 포맷 문자열|
|`object`|`{ parse: function(str) {...}, stringify: function(date) {...} }` 형태의 커스텀 파서·직렬화기|

### object 세부 옵션
|Name|Type|Description|
|---|---|---|
|`parse`|`function`|서버에서 받은 문자열을 **반드시 `Date` 객체 또는 timestamp(`number`)로 반환**해야 합니다.<br/>그 외 경우는 값이 `NaN`으로 저장되어 셀에 표시되지 않습니다.|
|`stringify`|`function`|Date 객체를 서버로 전송할 문자열로 변환합니다.|

### Example

**(1) 문자열 포맷 — 기본 사용**
```javascript
options.Cols = [
    {
      Type: "Date",
      Format: "yyyy.MM.dd HH:mm:ss",
      DataFormat: "yyyyMMddHHmmss",
      Name: "enterDate",
      Width: 120
    }
];
```

**(2) object 형식 — 커스텀 규격 예시**
```javascript
options.Cols = [
  {
    Name: "regDate", Type: "Date",
    DataFormat: {
      // 조회 시: 데이터가 '20260121 163151213'와 같은 형태로 들어온다고 가정
      // 서버 문자열 → Date객체(타임스탬프)로 리턴
      parse: function(str) {
        var s = ("" + str).replace(/\D/g, "");
        return new Date(+s.slice(0,4), +s.slice(4,6) - 1, +s.slice(6,8),
          +s.slice(8,10) || 0, +s.slice(10,12) || 0, +s.slice(12,14) || 0, +s.slice(14,17) || 0);
      },
      // 저장 시: Date객체(타임스탬프) → 서버 전송 문자열 리턴
      stringify: function(date) {
        var p = function(n, w) { return ("00" + n).slice(-(w || 2)); };
        return "" + date.getFullYear() + p(date.getMonth()+1) + p(date.getDate())
          + " " + p(date.getHours()) + p(date.getMinutes()) + p(date.getSeconds()) + p(date.getMilliseconds(), 3);
      }
    },
    Format: "yyyy-MM-dd HH:mm:ss.fff",
    EditFormat: "yyyy-MM-dd HH:mm:ss.fff"
  }
];
```

### Read More
- [DataFormat cell](/docs/props/cell/data-format)
- [DateStrictMode cfg](/docs/props/cfg/date-strict-mode)
- [Format col](/docs/props/col/format)
- [EditFormat col](/docs/props/col/edit-format)
- [Format appendix](/docs/appx/format)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.4.0.16|`f`(밀리초) / `z`(타임존) 예약어 지원, `object` 형식({parse, stringify}) 추가|
