# DataFormat ***(col)***
> `Date` 타입 컬럼에서 **서버에서 조회되는 날짜 데이터의 형식(format)** 을 지정합니다.  
> 예를 들어 조회 데이터가 `"25012017"` (25일 01월 2017년)이라면 `DataFormat: "ddMMyyyy"`로,  
> 조회 데이터가 `"20171225"` (25일 01월 2017년)라면 `DataFormat: "yyyyMMdd"`로 설정해야 합니다.  
> 해당 열의 데이터가 서버로 저장될 때 ([doSave](/docs/funcs/core/do-save), [getSaveString](/docs/funcs/core/get-save-string)) 지정된 `DataFormat` 형식으로 변환되어 전송됩니다.  
>
> `DataFormat`이 설정되지 않은 경우 날짜 데이터는 **표시 형식과 값 추출 형식이 서로 다르게 처리됩니다.**  
> 예를 들어 `getValue`는 `timestamp` 값으로 반환되며,  
> 저장 시에는 **Format이 적용된 화면 표시 값** 기준으로 처리됩니다.

### 날짜 예약어

|표시|의미|
|---|---|
|`yyyy`|년도(4자리)|
|`MM`|월(2자리)|
|`dd`|일(2자리)|
|`HH`|시간(2자리)|
|`mm`|분(2자리)|
|`ss`|초(2자리)|

### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`string`|`yyyyMMdd` 등 날짜 포맷 문자열|


### Example
```javascript
// Date 타입 컬럼의 조회 데이터 포맷 설정
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
