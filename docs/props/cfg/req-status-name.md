# ReqStatusName ***(cfg)***

<!-- synonyms: ReqStatusName, req status name, save status name, status field name, STATUS field, doSave status name, 상태 필드명, 상태 변수명, 저장 상태명, STATUS 컬럼, 서버 전송 상태명, Added Changed Deleted 이름 -->

> 저장 함수([doSave](/docs/funcs/core/do-save), [getSaveString](/docs/funcs/core/get-save-string), [getSaveJson](/docs/funcs/core/get-save-json)) 호출 시 각 행의 상태(`Added`, `Changed`, `Deleted`)를 전달하는 변수명을 설정합니다.  
> 별도의 설정이 없으면 `"STATUS"`로 전달됩니다.  
> 서버로 전달할 상태값은 `local/언어.js` 파일 안의 문자열(`"ReqStatusAdded": "Added"`(입력, Insert), `"ReqStatusChanged": "Changed"`(수정, Update), `"ReqStatusDeleted": "Deleted"`(삭제, Delete), `"ReqStatusEmpty": ""`(조회, Read))을 수정하면 됩니다.

### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`string`|서버로 전송될 상태 명 (`default: STATUS`)|


### Example
```javascript
options.Cfg = { "ReqStatusName": "mySheet_st" };
```

실제 서버로 전송 시 다음과 같이 전달됩니다.

```javascript
var saveStr = sheet.getSaveString();
//saveStr
//mySheet_st=Changed&ColName1=chris&ColName2=43 ...
```

### Read More
- [doSave method](/docs/funcs/core/do-save)
- [getSaveString method](/docs/funcs/core/get-save-string)
- [getSaveJson method](/docs/funcs/core/get-save-json)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
