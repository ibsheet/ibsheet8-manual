# getSaveJson ***(method)***

<!-- synonyms: 저장 JSON, JSON 추출, save json, 변경 데이터 추출 -->

> 시트 내에 변경된 내용(`입력(Added)`, `수정(Changed)`, `삭제(Deleted)`, `이동(Moved)`)을 JSON 형식의 객체로 추출합니다.  
> 추출한 데이터는 서버로 전송 후, 결과를 [acceptChangedData](/docs/funcs/core/accept-changed-data) 또는 [applySaveResult](/docs/funcs/core/apply-save-result)를 이용해 직접 시트에 반영해야 합니다.  
> 서버 응답 구조와 관련된 상세 내용은 [저장 응답 규격](/docs/dataStructure/saving-structure)을 참고하세요.  
> ajax 통신과 결과 반영을 자동 처리하려면 [doSave](./do-save)를 사용하세요.

### Syntax
```javascript
object getSaveJson( saveMode, col, validRequired, showAlert, saveAttr, useLevel, formData, saveExtraAttr, rows, validSize, validEditMask, validResultMask );
```

### Parameters

|Name|Type|Required| Description |
|----------|-----|---|----|
|saveMode|`number`|<span class='optional'>선택</span>|상태별 데이터 추출 여부 <br/>`0`:전체데이터<br>`1`:전체데이터 중 `Deleted` 만 제외<br>`2`:수정된 데이터(`Added`,`Changed`,`Deleted`) (`default`)<br>`3`:수정된 데이터(`Added`,`Changed`,`Deleted`)+이동한 데이터(`Moved`)|
|col|`string`|<span class='optional'>선택</span>|저장 기준 열의 열이름<br/>특정 열을 지정하면 행의 상태(`Added`,`Changed`,`Deleted`)를 무시하고 지정한 열의 데이터 유무에 따라 저장됨.|
|validRequired|`boolean`|<span class='optional'>선택</span>|데이터 필수 입력 항목([Required col](/docs/props/col/required) 설정된 열)에 대한 검사 여부 설정.<br/>`0(false)`:필수 입력 항목 검사 안함<br/>`1(true)`:필수 입력 항목 검사 실행 (`default`)<br/>**실패 시 `IBS010 RequiredError` 반환**|
|showAlert|`boolean`|<span class='optional'>선택</span>|`validRequired`, `validSize`, `validEditMask`, `validResultMask` 설정 시<br/>유효성 검사(Validation)를 통과하지 못한 경우 **메시지 표시 및 오류 셀 자동 포커스** 여부<br>`0(false)`:메시지/포커스 자동 처리 안 함. 검증 실패 시 첫 오류의 `Code`/`row`/`col`만 반환되며, 사용자가 직접 메시지/포커스 처리 필요 (`default`)<br>`1(true)`:메시지 표시 + 오류 셀에 자동 포커스<br/>![테이블](/assets/imgs/doSaveRequired1.png "테이블")<br/>![경고창](/assets/imgs/doSaveRequired2.png "경고창")<br/>※ 표시되는 메시지는 메세지 파일(예: `ko.js`등)에 정의된 내용을 사용합니다.<br/>(EditMaskError, SizeError, RequiredError, ResultMaskError)<br/>※ Cfg [ValidCheck](/docs/props/cfg/valid-check)가 활성화된 경우 이 옵션은 무시됩니다 (마킹 + 툴팁이 우선).|
|saveAttr|`string`|<span class='optional'>선택</span>|각 셀의 속성값을 같이 추출하고자 하는 경우 Name+속성명 형식으로 설정<br>여러개 속성을 추출하고자 하는 경우 ","를 구분자로 작성<br>ex) `"sNameColor,sNoCanEdit"`|
|useLevel|`boolean`|<span class='optional'>선택</span>|Tree기능 사용시 각 행의 Level(Depth)값을 추출되는 데이터에 포함할지 여부 (default: `1(true)`)<br><br>최 상위 노드를 1부터 시작하여 계산하며, `"tLEVEL"`이라는 이름으로 행 데이터에 추가됩니다.<br>`"tLEVEL"`은 각 메세지 파일(ex:`ko.js`)에서 `"TreeLevelName"`으로 변경할 수 있습니다.<br>Tree기능을 사용하는 시트에서 해당 속성을 `0(false)`로 설정시 `saveMode:0`을 통해 추출되는 데이터는 계층구조를 갖게 됩니다.<br/>`saveMode`를 이용하여 전체 데이터가 아닌 일부 데이터를 추출 할 경우 데이터는 계층 구조를 가지지 않으며 `"tLEVEL"` 값은 모두 1이 됩니다.|
|formData|`boolean`|<span class='optional'>선택</span>|저장 데이터를 Form Data로 추출 할지 여부 (default: `0(false)`)<br><br>***File 타입 저장 시 사용***|
|saveExtraAttr|`boolean`|<span class='optional'>선택</span>|시트에 (col)[Name](/docs/props/col/name)으로 정의하지 않은 데이터가 [doSearch](/docs/funcs/core/do-search)나 [loadSearchData](/docs/funcs/core/load-search-data)함수를 통해 로드 된 경우, 함수 호출시 해당 데이터를 같이 추출할 지 여부.<br>로드 데이터 첫번째 행의 keyset을 기준으로 추출됨.<br>`0(false)`:시트에 (col)[Name](/docs/props/col/name)으로 정의 되지 않은 데이터 서버 전송 시 미포함 (`default`)<br>`1(true)`:시트에 (col)[Name](/docs/props/col/name)으로 정의 되지 않은 데이터 서버 전송 시 포함|
|rows|`array[object]`|<span class='optional'>선택</span>| [데이터 로우 객체](/docs/appx/row-object) 배열로 입력한 행에 대한 정보를 추출합니다.  (default: `null`)|
|validSize|`boolean`|<span class='optional'>선택</span>|사이즈 설정([Size col](/docs/props/col/size))에 대한 유효성 검사 여부 설정.<br/>`0(false)`:사이즈 유효성 검사 안함 (`default`)<br/>`1(true)`:사이즈 유효성 검사 실행<br/>**실패 시 `IBS040 SizeError` 반환**|
|validEditMask|`boolean`|<span class='optional'>선택</span>|EditMask 설정([EditMask col](/docs/props/col/edit-mask))에 대한 유효성 검사 여부 설정.<br/>`0(false)`:EditMask 유효성 검사 안함 (`default`)<br/>`1(true)`:EditMask 유효성 검사 실행<br/>**실패 시 `IBS050 EditMaskError` 반환**|
|validResultMask|`boolean`|<span class='optional'>선택</span>|ResultMask 설정([ResultMask col](/docs/props/col/result-mask))에 대한 유효성 검사 여부 설정.<br/>`0(false)`:ResultMask 유효성 검사 안함 (`default`)<br/>`1(true)`:ResultMask 유효성 검사 실행<br/>**실패 시 `IBS060 ResultMaskError` 반환**|

정상적으로 데이터를 추출하지 못한 경우 다음 표의 `Code`와 `Message`가 반환됩니다.

| Code | Message         | Description |
|------| --------------- |-------------|
| `IBS000` |NoTargetRows | 저장 대상(`Added`, `Changed`, `Deleted`) 행이 없는 경우  |
| `IBS010` |RequiredError| `validRequired` 설정 시 필수 입력 항목 Validation 오류  |
| `IBS020` |InvalidRows  | `rows`에 지정한 행이 유효하지 않거나 처리 대상이 없는 경우 |
| `IBS030` |InvalidInputError | `onValidation` 이벤트에서 유효성 검사 기준에 맞지 않아 true를 반환한 경우 |
| `IBS040` |SizeError | `validSize` 설정 시 사이즈 Validation 오류인 경우 |
| `IBS050` |EditMaskError | `validEditMask` 설정 시 EditMask Validation 오류 |
| `IBS060` |ResultMaskError| `validResultMask` 설정 시 ResultMask Validation 오류 |

### Return Value
**json 형식의 object**
```json
// 정상적인 처리시
{
    "data":[
        {"id":"AR1","ColName1":"12345","ColName2":"ABCDE" ...},
        {"id":"AR4","ColName1":"76411","ColName2":"HIJKL" ...},
        ...
    ]
}

// validRequired 오류시
{
    "Message":"RequiredError",
    "Code":"IB010",
    "row":오류 발생 행 객체,
    "col":오류 발생 열 Name,
    "data":[]
}

// rows에 입력한 행 객체가 유효하지 않을 경우 
{
    "Message":"InvalidRows",
    "Code":"IB020",
    "data":[]
}
```


### Example
```javascript
// 수정 데이터 추출 + 유효성 검사
// showAlert:1 → 검사 실패 시 메시지 표시 + 오류 셀 자동 포커스
var saveJson = sheet.getSaveJson({
    validRequired: 1,
    validSize: 1,
    validEditMask: 1,
    showAlert: 1
});

// 유효성 검사 실패 또는 처리 대상 없음 → 저장 중단
if (saveJson.Code) return;

$.ajax({
    type: 'post',
    async: true,
    dataType: 'json',
    headers: { "X-Requested-With": "XMLHttpRequest" },
    contentType: "application/json; charset=utf-8",
    url: "/xgs/manage/sys/sawonTelSave.do",
    data: JSON.stringify(saveJson),
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
// showAlert 미사용 — 검증 실패 시 메시지/포커스를 직접 처리하는 패턴
var saveJson = sheet.getSaveJson({
    validRequired: 1,
    validSize: 1,
    validEditMask: 1
    // showAlert 생략 (default 0) → 사용자가 직접 처리
});

if (saveJson.Code) {
    // 검증 실패 → 첫 오류의 row/col 정보를 받아 직접 처리
    if (saveJson.row && saveJson.col) {
        alert(saveJson.Message);              // 또는 커스텀 메시지/UI 사용
        sheet.focus(saveJson.row, saveJson.col);
    }
    return; // 저장 중단
}

// 정상 → 서버 전송
$.ajax({ /* ... */ });
```

### Read More

- [Required col](/docs/props/col/required)
- [FormatFix col](/docs/props/col/format-fix)
- [acceptChangedData method](./accept-changed-data)
- [applySaveResult method](./apply-save-result)
- [doSave method](./do-save)
- [getSaveString method](./get-save-string)
- [ExcludeAddDelStatus cfg](/docs/props/cfg/exclude-add-del-status)
- [ReqStatusName cfg](/docs/props/cfg/req-status-name)
- [ValidCheck cfg](/docs/props/cfg/valid-check)
- [ValidateMessage cfg](/docs/props/cfg/validate-message)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.0.0.4|`saveAttr`,`useLevel` 기능 추가|
|core|8.0.0.5|`formData` 기능 추가|
|core|8.1.0.32|`saveExtraAttr` 기능 추가|
|core|8.1.0.43|`rows` 기능 추가|
|core|8.3.0.24|`validSize`, `validEditMask`, `validResultMask` 기능 추가|