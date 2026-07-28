# DateStrictMode ***(cfg)***

> `Date` 타입 컬럼에 `DataFormat`이 설정된 경우,  
> 조회된 날짜 값이 `DataFormat`과 일치하지 않거나 유효하지 않은 경우 해당 셀 값을 공백으로 처리합니다.  
> 엑셀 업로드 시 잘못된 날짜 데이터 검증(validation)에 유용합니다.

<!-- synonyms: date validation, strict date mode, invalid date 처리, 날짜 검증, date format validation -->


### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
| `0` (`false`) | 정밀 검사 미적용 (`default`) |
| `1` (`true`) | `DataFormat` 기준으로 날짜 정밀 검사 적용 |


### Example
```javascript
// 잘못된 날짜 데이터 조회 및 엑셀 업로드 시 공백 처리
options.Cfg = {
    DateStrictMode: 1
};
options.Cols = [
    // DateStrictMode를 사용하기 위해선 DataFormat이 설정되어야 합니다. 
    // 예: "88" 값이 조회되면 해당 셀은 공백으로 표시됩니다.
    {
        Type: "Date", 
        Format: "yyyy.MM.dd", 
        DataFormat: "yyyyMMdd", 
        Name: "enterDate"
    }
    
];
```

### Read More
- [DataFormat col](/docs/props/col/data-format)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.12|기능 추가|
