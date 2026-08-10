# CustomFormat ***(col)***

<!-- synonyms: 사용자 정의 포맷, 마스킹, 주민번호 마스킹, 카드번호 마스킹, 사업자번호 표시, 우편번호 형식, custom format, mask format, phone format, ssn mask, card mask -->

> 원본 데이터를 **마스킹(masking)하거나 특정 형식으로 표시하기 위한 사용자 정의 포맷**을 설정합니다.  
> `CustomFormat`은 [Type](/docs/appx/type)이 `Text` 또는 `Lines`인 열에서 사용할 수 있습니다.  
> 여러 개의 포맷을 `|` 구분자로 지정할 수 있으며, 사용자가 정의한 커스텀 포맷 함수도 지정할 수 있습니다.

### 예약어
|Value|Description|
|-----|-----|
|`#`|그대로 표시되는 문자|
|`*`|`*`(별표)로 마스킹되는 문자|
|`PostNo`|우편번호|
|`IdNoMask`|주민등록번호 (뒤 6자리는 `*` 처리)|
|`IdNo`|주민등록번호 전체 표시|
|`SaupNo`|사업자 등록번호|
|`CardNo`|카드번호|
|`PhoneNo`|전화번호(휴대폰번호, 안심번호)|


### Type
`mixed`( `string` \| `function` )

### Options
|Value|Description|
|-----|-----|
|`string` \| `function` |예약어 또는 사용자 정의 함수 |


### Example
```javascript

options.Cols = [
    
    //전화번호 포맷
    {Type: "Text", Name: "sPhone", CustomFormat: 'PhoneNo'}, 
    // 0226212288  → 02-2621-2288
    // 01073213834 → 010-7321-3834

    //임의의 포멧을 정의
    {Type: "Text", Name: "sawonNo", CustomFormat: '###-#####'}, 
    //12345678 → 123-45678

    //주민번호 마스킹
    {Type: "Text", Name: "cNo", CustomFormat: 'IdNoMask'}, 
    //8501242384211 → 850124-2******

    //카드번호 마스킹
    {"Type": "Text", "Name": "sCard", "CustomFormat": "[General] ####-####-####-####|[ Amex ] ####-######-#####"},

    // 데이터 길이에 따라 포맷 자동 적용
    {Type: "Text", Name: "cNo", CustomFormat: 'IdNoMask|SaupNo'}, 
    //주민번호  → 850124-2******
    //사업자번호  → 625-84-12458

    //사용자 정의 함수
    {Type: "Text", Name: "ISDNS", CustomFormat: function(v, sheet, col, row){
        // 조회 데이터에 포함된 '-' 제거(붙여넣기 시에도 동작)
        v = v.replace(/-/g, "");

        // 값의 길이에 따라 다른 포멧 적용
        if (v.length > 10) {
            return v.substr(0,6) + "-" + v.substr(6);
        } else {
            return v.substr(0,5) + "-" + v.substr(5);
        }

    }}
    
];
```

### Read More
- [Format appendix](/docs/appx/format)
- [Format col](./format)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.1.0.87|function 사용시 시트객체, 컬럼명 인자 추가|
|core|8.3.0.19|PhoneNo 포맷에 안심번호 추가|
|core|8.3.0.54|function 사용시 행 객체 인자 추가|
