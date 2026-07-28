# ValidCheck ***(cfg)***

<!-- synonyms: 유효성 검사, 검증 마킹, valid check, 저장 검증 -->

> 저장 함수([doSave](/docs/funcs/core/do-save), [getSaveJson](/docs/funcs/core/get-save-json), [getSaveString](/docs/funcs/core/get-save-string))의 유효성 검사(`validRequired`, `validSize`, `validEditMask`, `validResultMask`) 결과 처리 방식을 제어합니다.  
> `true` 또는 `object`로 설정하면 실패 셀을 빨간색([ColorState](./color-state) 32번, `.IBColorError`)으로 마킹하고 첫 실패 셀에 `focus` + 편집 상태를 적용하며  
> 마우스 오버 시 메시지 파일(예: `ko.js`)의 `RequiredError`/`SizeError`/`EditMaskError`/`ResultMaskError`가 툴팁으로 표시됩니다.  
> 추가 메시지가 필요하면 [ValidateMessage](./validate-message)를 함께 설정합니다.

### Type
`mixed`( `boolean` \| `object` )

### Options
|Value|Description|
|-----|-----|
|`0(false)`|마킹 없이 저장 함수 인자 동작에 위임 (`default`)<br/>`doSave`: `validRequired`/`validSize`/`validEditMask`/`validResultMask` 설정값에 따라 동작<br/>`getSaveJson`/`getSaveString`: `showAlert` 설정값에 따라 동작|
|`1(true)`|전체 데이터 검증 + 실패 셀 빨간색 일괄 마킹|
|`object`|`1(true)`와 동일 + 실패 첫 셀 동작 제어<br/>`Focus`(default: `1`): 자동 포커스 이동 여부<br/>`Edit`(default: `1`): 포커스 후 편집 상태 진입 여부|

### Example
```javascript
// 저장 함수(doSave, getSaveString, getSaveJson) 호출 시 유효성 검사를 수행합니다.
// 유효성 검사 실패한 제일 첫번째 셀에 Focus 이동, 셀을 편집 상태로 설정 합니다.
options.Cfg = {
    ValidCheck: true  
};

// 저장 함수(doSave, getSaveString, getSaveJson) 호출 시 유효성 검사를 수행합니다.
// 유효성 검사 실패한 제일 첫번째 셀에 Focus 이동합니다.
options.Cfg = {
    ValidCheck: {
        Focus : 1,
        Edit : 0
    },  
};
```

#### 시연 예제

4종 검증(`Required` / `Size` / `ResultMask` / `EditMask`)이 한 화면에서 마킹되는 전체 시트 예제입니다.

##### 컬럼 설정
```javascript
options.Cfg = {
    SearchMode: 0,
    ValidCheck: 1
};
options.Cols = [
    { Header: "ID",        Name: "sid",       Type: "Text", Width: 80,  Required: 1, Size: 5 },
    { Header: "e-mail",    Name: "eMail",     Type: "Text", Width: 180,
        ResultMask: "^[\\w\\.\\+%-]+@[A-Za-z0-9\\.-]+\\.[A-Za-z]{2,6}$",
        ResultMessage: "이메일 주소를 확인해 주세요.",
        ResultMessageTime: 1000 },
    { Header: "phone",     Name: "pNumber",   Type: "Text", Width: 140, EditMask: "^[0-9\\-]*$" },
    { Header: "Amount",    Name: "Amount",    Type: "Int",  Width: 100 },
    { Header: "StartDate", Name: "StartDate", Type: "Date", Width: 120, Format: "yyyy-MM-dd", DataFormat: "yyyyMMdd" },
    { Header: "EndDate",   Name: "EndDate",   Type: "Date", Width: 120, Format: "yyyy-MM-dd", DataFormat: "yyyyMMdd" }
];
```

##### 시연 데이터
```javascript
// Added:1 — 모든 행을 추가 상태로 만들어 저장 대상이 되도록 합니다 (그래야 ValidCheck가 마킹).
var data = {
    "Data": [
        { sid: "U01",    eMail: "alice@example.com", pNumber: "010-1111-2222", Amount: 1000, StartDate: "20260101", EndDate: "20260131", Added: 1 },
        { sid: "",       eMail: "bob@example.com",   pNumber: "010-2222-3333", Amount: 500,  StartDate: "",         EndDate: "20260228", Added: 1 },
        { sid: "USER06", eMail: "carol@example.com", pNumber: "010-3333-4444", Amount: 200,  StartDate: "20260301", EndDate: "20260331", Added: 1 },
        { sid: "U02",    eMail: "invalid-mail",      pNumber: "010-4444-5555", Amount: 700,  StartDate: "20260401", EndDate: "20260430", Added: 1 },
        { sid: "U03",    eMail: "dave@example.com",  pNumber: "010-abcd-efgh", Amount: 150,  StartDate: "20260501", EndDate: "20260531", Added: 1 }
    ]
};
sheet.loadSearchData(data);
```

##### 검증 결과
| 행 | 빨간 마킹 셀 | 호버 툴팁 |
|---|---|---|
| 1 | 없음 | — |
| 2 | sid | RequiredError |
| 3 | sid | SizeError |
| 4 | eMail | ResultMaskError |
| 5 | pNumber | EditMaskError |

##### 화면

![ValidCheck 마킹](/assets/imgs/validCheckMark.png "ValidCheck 마킹")
![호버 툴팁](/assets/imgs/validCheckTooltip.png "호버 툴팁")


### Read More
- [doSave method](/docs/funcs/core/do-save)
- [getSaveJson method](/docs/funcs/core/get-save-json)
- [getSaveString method](/docs/funcs/core/get-save-string)
- [ValidateMessage cfg](/docs/props/cfg/validate-message)
- [ColorState cfg](./color-state)
- [Required col](/docs/props/col/required)
- [Size col](/docs/props/col/size)
- [EditMask col](/docs/props/col/edit-mask)
- [ResultMask col](/docs/props/col/result-mask)

### Since

|product|version|desc|
|---|---|---|
|core|8.2.0.3|기능 추가|
|core|8.2.0.15|`object` 기능 추가|
