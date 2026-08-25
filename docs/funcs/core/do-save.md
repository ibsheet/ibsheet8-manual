# doSave ***(method)***

<!-- synonyms: 저장, 데이터 저장, 대기이미지, 로딩, save, data save, loading, ajax -->

> `doSave`는 시트의 변경된 데이터를 자동으로 추출하여 AJAX 통신으로 서버에 전송하고, 서버 응답을 시트에 자동 반영합니다.  
> 기본 전송 형식은 querystring([getSaveString](./get-save-string)과 동일)이며, `queryMode: 0` 설정 시 JSON([getSaveJson](./get-save-json)과 동일)으로 전송합니다.  
> 데이터 추출만 하고 AJAX 통신은 직접 처리하려면 [getSaveJson](./get-save-json) 또는 [getSaveString](./get-save-string)을 사용하세요.  
> 비동기로 동작하므로, 전송 전 처리는 [onBeforeSave](/docs/events/on-before-save), 응답 후 처리는 [onAfterSave](/docs/events/on-after-save) 이벤트에서 구현하세요.  
> 서버 응답 구조와 관련된 상세 내용은 [저장 응답 규격](/docs/dataStructure/saving-structure)을 참고하세요.  
> 저장 시 메시지 표시는 [(Cfg)SuppressMessage](/docs/props/cfg/suppress-message)를 참고하세요.

### Syntax
```javascript
void doSave( url, param, saveMode, col, urlEncode, delim, queryMode, reqHeader, quest, sync, validRequired, saveAttr, useLevel, questCallback, timeout, traditional, saveExtraAttr, validSize, validEditMask, validResultMask );
```

### Parameters

|Name|Type|Required|Description|
|----------|-----|---|----|
|url|`string`|<span class='required'>필수</span>|ajax를 통해 호출할 url|
|param|`string` \| `object`|<span class='optional'>선택</span>|서버로 전송할 파라미터|
|saveMode|`number`|<span class='optional'>선택</span>|상태별 데이터 추출 여부 <br/>`0`:전체데이터<br>`1`:전체데이터 중 `Deleted` 만 제외<br>`2`:수정된 데이터(`Added,Changed,Deleted`) (`default`)<br>`3`:수정된 데이터(`Added,Changed,Deleted`)+이동한 데이터(`Moved`)|
|col|`string`|<span class='optional'>선택</span>|저장 기준 열의 열이름<br/>특정 열을 지정하면 행의 상태(`Added,Changed,Deleted`)를 무시하고 지정한 열의 데이터 유무에 따라 저장됨.|
|urlEncode|`boolean`|<span class='optional'>선택</span>|시트의 데이터에 대한 encoding 여부 <br/> **`queryMode`별로 `default`가 달라짐** <br/>`0(false)`:`queryMode:0 (default)`<br/>`1(true)`:`queryMode:1/2 (default)`<br/>|
|delim|`string`|<span class='optional'>선택</span>|queryMode값이 2인 경우에 데이터 사이 구분자 지정 (`default: "\|"`)|
|queryMode|`number`|<span class='optional'>선택</span>|서버로 전달될 데이터 구조 설정<br/>**`0`:json 구조로 전달**<br/>ex)<br/>Data={<br/>"data":[<br/>{"STATUS":"Added","ColName1":"홍길동","ColName2":25},<br/>{"STATUS":"Changed","ColName1":"심청","ColName2":18}<br/>]}<br/>*단 **reqHeader**속성에 {"Content-Type":"application/json"}를 추가시 앞에 "Data="이 제거되고 순수하게 json형식만 서버로 전송*<br/>**`1`:QueryString 구조 전달** (`default`)<br/>ex)<br/>STATUS=Added&ColName1=홍길동&ColName2=25&STATUS=Changed&ColName1=심청&ColName2=18<br/>**`2`:열데이터 기준 QueryString 구조 전달**<br/>ex)<br/>STATUS=Added\|Changed&ColName1=홍길동\|심청&ColName2=25\|18|
|reqHeader|`object`|<span class='optional'>선택</span>|전송시 request header에 추가하고자 하는 내용 (ex) {key1:value1, key2:value2})<br>[Type](/docs/props/col/type)이 file인 셀의 값이 수정된 경우 reqHeader에 Content-Type:application/json을 설정하여도 form으로 전송됩니다.
|quest|`boolean`|<span class='optional'>선택</span>|저장시 confirm 메세지 사용 여부<br/>`0(false)`:confirm 메세지 사용 안함 (`default`)<br/>`1(true)`:confirm 메세지 사용<br/>![경고창](/assets/imgs/quest.png "경고창")<br/>확인창 문구는 메시지 파일(ko.js 등)의 `ConfirmSaveDataRows`이며, [setMessage](./set-message)로 변경할 수 있습니다.|
|sync|`boolean`|<span class='optional'>선택</span>|저장시 동기 여부<br/>`0(false)`:비동기 방식 (`default`)<br/>`1(true)`:동기 방식|
|validRequired|`boolean`|<span class='optional'>선택</span>|데이터 필수 입력 항목([Required col](/docs/props/col/required) 설정된 열)에 대한 검사 여부 설정. 검사를 통과하지 못할 시 메시지를 띄우며 편집모드 실행.<br/>`0(false)`:필수 입력 항목 검사 안함<br/>`1(true)`:필수 입력 항목 검사 실행 (`default`)<br/>![테이블](/assets/imgs/doSaveRequired1.png "테이블")<br/>![경고창](/assets/imgs/doSaveRequired2.png "경고창")<br/>※ Cfg [ValidCheck](/docs/props/cfg/valid-check)가 활성화된 경우 메시지/편집모드 대신 마킹 + 툴팁으로 표시됩니다.|
|saveAttr|`string`|<span class='optional'>선택</span>|각 셀의 속성값을 같이 추출하고자 하는 경우 Name+속성명 형식으로 설정<br>여러개 속성을 추출하고자 하는 경우 ","를 구분자로 작성<br>ex) "sNameColor,sNoCanEdit"|
|useLevel|`boolean`|<span class='optional'>선택</span>|Tree기능 사용시 각 행의 Level(Depth)값을 추출되는 데이터에 포함할지 여부<br/>`0(false)`:Level값 데이터 미포함<br/>`1(true)`:Level값 데이터 포함(`default`)<br>최 상위 노드를 1부터 시작하여 계산하며, "tLEVEL"이라는 이름으로 행 데이터에 추가됩니다.<br>"tLEVEL"은 각 메세지 파일(ex: ko.js)에서 "TreeLevelName"으로 변경할 수 있습니다.<br>Tree기능을 사용하는 시트에서 해당 속성을 `0(false)`로 설정시 `saveMode:0, queryMode:0`을 통해 추출되는 데이터는 계층구조를 갖게 됩니다.<br/>`saveMode`를 이용하여 전체 데이터가 아닌 일부 데이터를 추출 할 경우 데이터는 계층 구조를 가지지 않으며 `"tLEVEL"` 값은 모두 1이 됩니다.|
|questCallback|`function`|<span class='optional'>선택</span>|confirm 메세지 사용시(`quest:true`) Ok, Cancel에 대한 콜백 함수<br/> Ok(확인) : `{result:1}` <br/> Cancel(취소) : `{result:2}` |
|timeout|`number`|<span class='optional'>선택</span>|서버 통신 최대 대기 시간 (단위: 초(second), `default: 60`)|
|traditional|`boolean`|<span class='optional'>선택</span>|서버로 전달될 param 구조 설정<br/>`param: {"data": [1, 2]}` 배열 구조 param 전송시 설정<br/>**`0(false)`:[] 을 포함하여 전송** (`default`)<br/>ex) `data[]=1&data[]=2`<br/>**`1(true)`:[] 없이 전송**<br/>ex) `data=1&data=2`<br/>|
|saveExtraAttr|`boolean`|<span class='optional'>선택</span>|시트에 (col)[Name](/docs/props/col/name)으로 정의하지 않은 데이터가 [doSearch](/docs/funcs/core/do-search)나 [loadSearchData](/docs/funcs/core/load-search-data)함수를 통해 로드 된 경우, 저장시 해당 데이터를 서버로 전송할 지 여부.<br>로드 데이터 첫번째 행의 keyset을 기준으로 추출됨.<br>`0(false)`:시트에 (col)[Name](/docs/props/col/name)으로 정의 되지 않은 데이터 서버 전송 시 미포함 (`default`)<br>`1(true)`:시트에 (col)[Name](/docs/props/col/name)으로 정의 되지 않은 데이터 서버 전송 시 포함|
|validSize|`boolean`|<span class='optional'>선택</span>|사이즈 설정([Size col](/docs/props/col/size))에 대한 유효성 검사 여부 설정. 검사 실패 시 메시지를 띄우며 편집모드 실행.<br/>`0(false)`:사이즈 유효성 검사 안함 (`default`)<br/>`1(true)`:사이즈 유효성 검사 실행<br/>※ Cfg [ValidCheck](/docs/props/cfg/valid-check)가 활성화된 경우 메시지/편집모드 대신 마킹 + 툴팁으로 표시됩니다.|
|validEditMask|`boolean`|<span class='optional'>선택</span>|EditMask 설정([EditMask col](/docs/props/col/edit-mask))에 대한 유효성 검사 여부 설정. 검사 실패 시 메시지를 띄우며 편집모드 실행.<br/>`0(false)`:EditMask 유효성 검사 안함 (`default`)<br/>`1(true)`:EditMask 유효성 검사 실행<br/>※ Cfg [ValidCheck](/docs/props/cfg/valid-check)가 활성화된 경우 메시지/편집모드 대신 마킹 + 툴팁으로 표시됩니다.|
|validResultMask|`boolean`|<span class='optional'>선택</span>|ResultMask 설정([ResultMask col](/docs/props/col/result-mask))에 대한 유효성 검사 여부 설정. 검사 실패 시 메시지를 띄우며 편집모드 실행.<br/>`0(false)`:ResultMask 유효성 검사 안함 (`default`)<br/>`1(true)`:ResultMask 유효성 검사 실행<br/>※ Cfg [ValidCheck](/docs/props/cfg/valid-check)가 활성화된 경우 메시지/편집모드 대신 마킹 + 툴팁으로 표시됩니다.|

### Return Value
***none***

### Example
```javascript
// 인자가 많으므로 객체 형식 사용 권장
sheet.doSave({
  url: "./insaAppMain.do",
  param: "dept_cd=031&position_cd=A0",
  quest: 1,
  questCallback: function(evt) {
    if (evt.result == 2) {
      alert("취소 되었습니다.");
    }
  }
});
```

### Read More
- [저장 응답 규격](/docs/dataStructure/saving-structure)
- [Required col](/docs/props/col/required)
- [FormatFix col](/docs/props/col/format-fix)
- [onValidation event](/docs/events/on-validation)
- [onSave event](/docs/events/on-save)
- [onBeforeSave event](/docs/events/on-before-save)
- [onAfterSave event](/docs/events/on-after-save)
- [getSaveJson method](./get-save-json)
- [getSaveString method](./get-save-string)
- [ExcludeAddDelStatus cfg](/docs/props/cfg/exclude-add-del-status)
- [ReqStatusName cfg](/docs/props/cfg/req-status-name)
- [Timeout cfg](/docs/props/cfg/timeout)
- [SuppressMessage cfg](/docs/props/cfg/suppress-message)
- [ValidCheck cfg](/docs/props/cfg/valid-check)
- [ValidateMessage cfg](/docs/props/cfg/validate-message)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.0.0.4|`saveAttr`, `useLevel` 기능 추가|
|core|8.0.0.5|`timeout` 기능 추가<br>`reqHeader` 설명 추가(`file` 타입 관련)|
|core|8.0.0.7|`traditional` 기능 추가|
|core|8.1.0.32|`saveExtraAttr` 기능 추가|
|core|8.3.0.24|`validSize`, `validEditMask`, `validResultMask` 기능 추가|