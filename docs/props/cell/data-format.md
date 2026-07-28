# DataFormat ***(cell)***

> [Type](/docs/appx/type)이 `Date`인 셀에 **서버에서 조회되는 날짜 데이터의 형식(format)** 을 지정합니다.  
> 예를 들어 조회 데이터가 `"25012017"` (25일 01월 2017년)이라면 `DataFormat: "ddMMyyyy"`로,  
> 조회 데이터가 `"20171225"` (2017년 12월 25일)이라면 `DataFormat: "yyyyMMdd"`로 설정해야 합니다.  
>
> 시트에서 수정된 데이터가 서버로 저장될 때 ([doSave](/docs/funcs/core/do-save), [getSaveString](/docs/funcs/core/get-save-string)) 지정된 `DataFormat` 형식으로 변환되어 전달됩니다.  
> **자세한 내용은 appendix의 [Format](/docs/appx/format)을 참고해 주세요.**

### 날짜 예약어

|표시|의미|
|---|---|
|`yyyy`|년도 (4자리)|
|`MM`|월 (2자리)|
|`dd`|일 (2자리)|
|`HH`|시간 (2자리)|
|`mm`|분 (2자리)|
|`ss`|초 (2자리)|

### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`string`|`yyyyMMdd` 등 날짜 포맷 문자열|

### Example
```javascript
//1. setAttribute 함수를 통해 특정 셀의 DataFormat 변경
sheet.setAttribute(sheet.getRowById("AR9"), "EDate", "DataFormat", "yyyyMMdd");

//변경내용 확인 (수정한 포맷으로 데이터 추출됨)
var json = sheet.getSaveJson();


//2. 객체에 직접 접근하여 DataFormat 변경 (CLS열의 DataFormat을 "yyyyMMddHHmm"로 변경)
var ROW = sheet.getRowById("AR10");
ROW["CLSDataFormat"] = "yyyyMMddHHmm";

//변경내용 확인
var json = sheet.getSaveJson();


//3. 조회 데이터 내에서 DataFormat 변경
{
    data:[
        {"CLS":"12312018", "CLSDataFormat":"MMddyyyy" }
    ]
}
```

### Read More
- [DataFormat col](/docs/props/col/data-format)
- [Format cell](./format)
- [EditFormat cell](./edit-format)
- [Format appendix](/docs/appx/format)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
