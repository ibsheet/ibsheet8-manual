# getFilter ***(method)***

<!-- synonyms: getFilter, get-filter, 필터 조회, 필터 확인, 필터 값, 필터 설정 조회, 필터행, 필터 상태, filter -->

> 필터행에 설정한 내용을 확인합니다.

### Syntax
```javascript
object getFilter( spec );
```

### Parameters
|Name|Type|Required| Description |
|----------|-----|---|----|
|spec|`boolean`|<span class='optional'>선택</span>|일반필터 와 [setFilter](./set-filter)에 대한 내용 여부<br/>`0(false)`:일반필터 설정 (`default`)<br>`1(true)`:setFilter 설정|

### Return Value
***object*** : 필터 설정 값(이차원 배열)
|입력값|유형|리턴 데이터 형식|
|---|---|---|
|`0`|일반필터|`[["colName1" , "필터값" , 연산자 ], ["colName2","필터값",연산자] ...]`|
|`1`|setFilter|`[["필터명", "cardAmt>=5000?1:0"], ["필터명", "deptNm=='자재부서'?1:0"] ...]`|



### Example
```javascript
//필터 초기화
var filterDesc = sheet.getFilter(0);
```

### Read More
- [setFilter method](./set-filter)
- [doFilter method](./do-filter)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
