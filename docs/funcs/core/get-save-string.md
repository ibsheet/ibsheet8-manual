# getSaveString ***(method)***

<!-- synonyms: 저장 문자열, querystring 추출, save string, 변경 데이터 추출 -->

> 시트 내에 변경된 내용(`입력(Added)`, `수정(Changed)`, `삭제(Deleted)`, `이동(Moved)`)을 querystring 형식의 문자열로 추출합니다.  
> 추출한 데이터는 서버로 전송 후, 결과를 [acceptChangedData](/docs/funcs/core/accept-changed-data) 또는 [applySaveResult](/docs/funcs/core/apply-save-result)를 이용해 직접 시트에 반영해야 합니다.  
> 서버 응답 구조와 관련된 상세 내용은 [저장 응답 규격](/docs/dataStructure/saving-structure)을 참고하세요.  
> JSON 형식 결과는 [getSaveJson](./get-save-json), ajax 통신과 결과 반영을 자동 처리하려면 [doSave](./do-save)를 사용하세요.

### Syntax
```javascript
string getSaveString( saveMode, col, urlEncode, delim, queryMode, validRequired, prefix, showAlert, saveAttr, saveExtraAttr, validSize, validEditMask, validResultMask );
```

### Parameters

|Name|Type|Required| Description |
|----------|-----|---|----|
|saveMode|`number`|<span class='optional'>선택</span>|상태별 데이터 추출 여부 <br/>`0`:전체데이터<br>`1`:전체데이터 중 `Deleted` 만 제외<br>`2`:수정된 데이터(`Added`,`Changed`,`Deleted`) (`default`)<br>`3`:수정된 데이터(`Added`,`Changed`,`Deleted`)+이동한 데이터(`Moved`)|
|col|`string`|<span class='optional'>선택</span>|저장 기준 열의 열이름<br/>특정 열을 지정하면 행의 상태(`Added`,`Changed`,`Deleted`)를 무시하고 지정한 열의 데이터 유무에 따라 저장됨.|
|urlEncode|`boolean`|<span class='optional'>선택</span>|조합되는 문자열의 인코딩 여부(encodeURIComponent로 문자열을 인코딩함 )<br/> **`queryMode`별로 `default`가 달라짐** <br/>`0(false)`:`queryMode:0 (default)`<br/>`1(true)`:`queryMode:1/2 (default)`|
|delim|`string`|<span class='optional'>선택</span>|queryMode값이 2인 경우에 데이터 사이 구분자 지정 (`default : "\|"`)|
|queryMode|`number`|<span class='optional'>선택</span>|서버로 전달될 데이터 구조 설정<br/>**`0`:json 구조로 전달**<br/>ex)<br/>Data={<br/>"data":[<br/>{"STATUS":"Added","ColName1":"홍길동","ColName2":25},<br/>{"STATUS":"Changed","ColName1":"심청","ColName2":18}<br/>]}<br/>*단 **reqHeader**속성에 {"Content-Type":"application/json"}를 추가시 앞에 "Data="이 제거되고 순수하게 json형식만 서버로 전송*<br/>**`1`:QueryString 구조 전달** (`default`)<br/>ex)<br/>STATUS=Added&ColName1=홍길동&ColName2=25&STATUS=Changed&ColName1=심청&ColName2=18<br/>**`2`:열데이터 기준 QueryString 구조 전달**<br/>ex)<br/>STATUS=Added\|Changed&ColName1=홍길동\|심청&ColName2=25\|18|
|validRequired|`boolean`|<span class='optional'>선택</span>|데이터 필수 입력 항목([Required col](/docs/props/col/required) 설정된 열)에 대한 검사 여부<br/>`0(false)`:필수 입력 항목 검사 안함<br/>`1(true)`:필수 입력 항목 검사 실행 (`default`)<br/>**실패 시 `IBS010 RequiredError` 반환**|
|prefix|`string`|<span class='optional'>선택</span>|열의 이름 앞에 설정할 문자열<br/>여러개 시트를 한번에 서버로 보낼때 시트id_colName 형식으로 보낼 수 있음<br/>ex) `sheet_saName=홍길동&sheet_saId=839212` 식으로 queryString이 만들어짐<br/>(`default : ""`)|
|showAlert|`boolean`|<span class='optional'>선택</span>|`validRequired`, `validSize`, `validEditMask`, `validResultMask` 설정 시<br/>유효성 검사(Validation)를 통과하지 못한 경우 **메시지 표시 및 오류 셀 자동 포커스** 여부<br>`0(false)`:메시지/포커스 자동 처리 안 함. 검증 실패 시 결과 문자열에 오류 정보(`Message\|Code\|행id\|열명`)만 포함되며, 사용자가 직접 메시지/포커스 처리 필요 (`default`)<br>`1(true)`:메시지 표시 + 오류 셀에 자동 포커스<br/>![테이블](/assets/imgs/doSaveRequired1.png "테이블")<br/>![경고창](/assets/imgs/doSaveRequired2.png "경고창")<br/>※ 표시되는 메시지는 메세지 파일(예: `ko.js`등)에 정의된 내용을 사용합니다.<br/>(EditMaskError, SizeError, RequiredError, ResultMaskError)<br/>※ Cfg [ValidCheck](/docs/props/cfg/valid-check)가 활성화된 경우 이 옵션은 무시됩니다 (마킹 + 툴팁이 우선).|
|saveAttr|`string`|<span class='optional'>선택</span>|각 셀의 속성값을 같이 추출하고자 하는 경우 Name+속성명 형식으로 설정<br>여러개 속성을 추출하고자 하는 경우 ","를 구분자로 작성<br>ex) `"sNameColor,sNoCanEdit"`|
|saveExtraAttr|`boolean`|<span class='optional'>선택</span>|시트에 (col)[Name](/docs/props/col/name)으로 정의하지 않은 데이터가 [doSearch](/docs/funcs/core/do-search)나 [loadSearchData](/docs/funcs/core/load-search-data)함수를 통해 로드 된 경우, 함수 호출시 해당 데이터를 같이 추출할 지 여부.<br>로드 데이터 첫번째 행의 keyset을 기준으로 추출됨<br>`0(false)`:시트에 (col)[Name](/docs/props/col/name)으로 정의 되지 않은 데이터 서버 전송 시 미포함 (`default`)<br>`1(true)`:시트에 (col)[Name](/docs/props/col/name)으로 정의 되지 않은 데이터 서버 전송 시 포함|
|validSize|`boolean`|<span class='optional'>선택</span>|사이즈 설정([Size col](/docs/props/col/size))에 대한 유효성 검사 여부 설정.<br/>`0(false)`:사이즈 유효성 검사 안함 (`default`)<br/>`1(true)`:사이즈 유효성 검사 실행<br/>**실패 시 `IBS040 SizeError` 반환**|
|validEditMask|`boolean`|<span class='optional'>선택</span>|EditMask 설정([EditMask col](/docs/props/col/edit-mask))에 대한 유효성 검사 여부 설정.<br/>`0(false)`:EditMask 유효성 검사 안함 (`default`)<br/>`1(true)`:EditMask 유효성 검사 실행<br/>**실패 시 `IBS050 EditMaskError` 반환**|
|validResultMask|`boolean`|<span class='optional'>선택</span>|ResultMask 설정([ResultMask col](/docs/props/col/result-mask))에 대한 유효성 검사 여부 설정.<br/>`0(false)`:ResultMask 유효성 검사 안함 (`default`)<br/>`1(true)`:ResultMask 유효성 검사 실행<br/>**실패 시 `IBS060 ResultMaskError` 반환**|

정상적으로 데이터를 추출하지 못한 경우 다음 표와 같은 결과가 반환됩니다.

| Code | Message         | Description |
|------| --------------- |-------------|
| `""` | — | 저장 대상(`Added`, `Changed`, `Deleted`) 행이 없는 경우 (빈 문자열 반환) |
| `IBS010` |RequiredError| `validRequired` 설정 시 필수 입력 항목 Validation 오류  |
| `IBS030` |InvalidInputError | `onValidation` 이벤트에서 유효성 검사 기준에 맞지 않아 true를 반환한 경우 |
| `IBS040` |SizeError | `validSize` 설정 시 사이즈 Validation 오류인 경우 |
| `IBS050` |EditMaskError | `validEditMask` 설정 시 EditMask Validation 오류 |
| `IBS060` |ResultMaskError| `validResultMask` 설정 시 ResultMask Validation 오류 |

### Return Value
**String**
```json
// 정상적인 처리시(querystring 형태)
"sa_name=홍길동&sa_id=02712&sa_dept=031&..."

// 저장(Added, Changed, Deleted) 대상이 없는 경우
""

// validRequired 설정 시 Validation 오류인 경우  
"RequiredError|IBS010|오류발생 행 id|오류발생 열 Name"
```
<!--| 결과 | Description |
|------|-------------|
|sa_name=홍길동&sa_id=02712&sa_dept=031&...| 정상 처리일 경우(querystring 형태) |
|""| 저장(Added, Changed, Deleted) 대상이 없는 경우 |
|RequiredError\|IBS010\|오류발생 행 id\|오류발생 열 Name| `validRequired` 설정 시 Validation 오류인 경우  |-->

### Example
```javascript
// 수정 데이터 추출 + 유효성 검사
// showAlert:1 → 검사 실패 시 메시지 표시 + 오류 셀 자동 포커스
var saveStr = sheet.getSaveString({
    validRequired: 1,
    validSize: 1,
    validEditMask: 1,
    showAlert: 1
});

// 빈 문자열 → 저장 대상 없음 (showAlert 무관, 사용자에게 별도 안내 필요)
if (saveStr === "") {
    alert("변경사항이 없습니다.");
    return;
}

// 검증 실패 → "Error|IBS...." 형식 (showAlert:1이라 메시지/포커스는 IBSheet가 자동 처리)
if (saveStr.indexOf("Error|") > -1) return;

$.ajax({
    type: 'post',
    url: "sheetSaveWorx.do",
    data: saveStr,
    success: function(data) {
        // applySaveResult가 IO.Result에 따라 분기 처리 (성공 시 상태 클리어, 실패 시 메시지)
        sheet.applySaveResult(data.IO.Result, data.IO.Message);
    },
    error: function(data, status, err) {
        alert('서버와의 통신이 실패했습니다.');
    }
});
```

```javascript
// showAlert 미사용 — 검증 실패 시 결과 문자열을 직접 파싱하는 패턴
var saveStr = sheet.getSaveString({
    validRequired: 1,
    validSize: 1,
    validEditMask: 1
    // showAlert 생략 (default 0) → 사용자가 직접 처리
});

if (saveStr === "") {
    alert("변경사항이 없습니다.");
    return;
}

// "Message|Code|행id|열명" 형식 파싱
if (saveStr.indexOf("Error|") > -1) {
    var parts = saveStr.split("|");
    var message = parts[0];   // 예: "RequiredError"
    var rowId   = parts[2];   // 예: "AR3"
    var colName = parts[3];   // 예: "sa_name"

    alert(message);                                // 또는 커스텀 메시지/UI
    sheet.focus(sheet.getRowById(rowId), colName);
    return;
}

$.ajax({ /* ... */ });
```

### Read More

- [저장 응답 규격](/docs/dataStructure/saving-structure)
- [Required col](/docs/props/col/required)
- [FormatFix col](/docs/props/col/format-fix)
- [acceptChangedData method](./accept-changed-data)
- [applySaveResult method](./apply-save-result)
- [doSave method](./do-save)
- [getSaveJson method](./get-save-json)
- [ExcludeAddDelStatus cfg](/docs/props/cfg/exclude-add-del-status)
- [ReqStatusName cfg](/docs/props/cfg/req-status-name)
- [getChangedData method](./get-changed-data)
- [onValidation event](/docs/events/on-validation)
- [SuppressMessage cfg](/docs/props/cfg/suppress-message)
- [ValidCheck cfg](/docs/props/cfg/valid-check)
- [ValidateMessage cfg](/docs/props/cfg/validate-message)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.0.0.4|`saveAttr` 기능 추가|
|core|8.1.0.32|`saveExtraAttr` 기능 추가|
|core|8.3.0.24|`validSize`, `validEditMask`, `validResultMask` 기능 추가|