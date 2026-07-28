# create ***(static)***

> 지정한 위치에 시트객체를 생성합니다.<br/>
> 시트객체가 생성되면 `IBSheet`객체에 배열형식으로 추가(push)됩니다.<br/>


- 'el' <mark>객체의 크기</mark>에 따라 시트의 너비/높이가 결정됩니다.
- 'el'객체의 너비/높이가 정의되지 않은 경우에는 <mark>너비는 100%, 높이는 800px</mark>로 설정됩니다.
- sync속성을 1로 사용 시 onRenderFirstFinish 이벤트에서는 window[id] 형식으로 시트에 접근할 수없습니다.(evtParam.sheet로만 접근 가능)

### Syntax
```javascript
object IBSheet.create(id, el, options, data, sync);
```

### Parameters
|Name|Type|Required|Description|
|----------|-----|---|----|
|id|`string`|<span class='required'>필수</span>|시트객체의 `id` (여기서 지정한 `id`는 `window` 객체에 `프로퍼티`로 생성됩니다.[전역변수]|
|el|`string`|<span class='required'>필수</span>|시트객체가 생성될 div객체의 `id` (해당객체 안에 시트객체가 생성됨)|
|[options](/docs/start/basic-structure)|`object`|<span class='required'>필수</span>|초기화 정보를 갖고있는 `json 객체`|
|data|`array[object]`|<span class='optional'>선택</span>|생성과 동시에 로드 될 `데이터 배열`|
|sync|`boolean`|<span class='optional'>선택</span>|시트를 동기로 생성합니다<br/>`0(false)`:비동기 방식 (`default`)<br/>`1(true)`:동기 방식|

### Return Value
***object***

### Example
```javascript
var opt = {
        //각 열에 대한 정의 (열의 이름, 유형(Type), 포맷(Format)등을 설정)
        Cols:[
            {Header: {Value: "이름"}, Name: "sa_nm", Type: "Text"},
            {Header: {Value: "사원번호" }, Name: "sa_id", Type: "Text", Align: "center"},
            {Header: {Value: "부서"}, Name: "sa_dept", Type: "Enum",
                Enum: "|경영지원|총무|인사|설계|시공1|시공2", EnumKeys: "|01|02|03|04|05|06"},
            {Header: {Value: "직급"}, Name: "sa_position", Type: "Enum",
                Enum: "|대표|상무|이사|부장|차장|과장|대리|사원", EnumKeys: "|A1|A2|A3|B0|B1|C4|C5|C6"},
            {Header: {Value: "입사일"}, Name: "sa_enterdate", Type: "Date",Width:100, Format: "yyyy/MM/dd"},
            {Header: {Value: "비고"}, Name: "sa_desc", Type: "Lines"}
        ]
    };
var dataArr = [
    {sa_nm: "홍길동", sa_id: "9821450", sa_dept: "04", sa_position: "B0", sa_enterdate: "19980305", sa_desc: ""},
    {sa_nm: "김한국", sa_id: "9510427", sa_dept: "01", sa_position: "A3", sa_enterdate: "19890317", sa_desc: ""}
];

//시트객체 생성
IBSheet.create({
    id: "sheet", // 생성할 시트의 id
    el: "sheetDiv", // 시트를 생성할 Dom 객체 및 id
    options: opt, // 생성될 시트의 속성
    data: dataArr, // 생성될 시트의 정적데이터
    sync: 1 // 동기로 시트 생성( 비동기로 시트 생성)
});

//el에 html element 설정
IBSheet.create({
    "id": "sheet", // 시트객체 이름 (SPA에서는 사용 X)
    "el": document.querySelector("div.part1 .gridarea"), // 시트를 생성할 html element 
    "options": opt, // 초기화 구문
    "data": dataArr//초기 데이터
});
```
### 생성 흐름 (라이프사이클)

`IBSheet.create()`를 호출하면 아래 순서로 시트가 만들어집니다.

1. `IBSheet.create()` 호출
2. [IBSheet.CommonOptions (static)](./common-options)와 호출 시 전달한 `options`가 머지됨
3. [IBSheet.onBeforeCreate (static)](./on-before-create) 훅이 정의되어 있으면 실행 — 머지된 옵션을 최종 수정 (반드시 수정된 객체를 `return`)
4. 시트 객체 생성 및 최초 렌더링
5. [onRenderFirstFinish (event)](/docs/events/on-render-first-finish) 발생 (최초 1회) — 이 시점부터 시트를 사용할 수 있음

생성 과정에서 발생하는 렌더 이벤트 순서는 다음과 같습니다.

|순서|이벤트|설명|
|---|---|---|
|1|`onRenderStart`|시트를 렌더링하기 전에 발생|
|2|`onRenderFinish`|시트가 렌더링된 후 발생|
|3|[onRenderFirstFinish](/docs/events/on-render-first-finish)|시트가 처음 생성되어 렌더링될 때 발생 (최초 1회만)|

`onRenderStart`와 `onRenderFinish`는 생성뿐 아니라 조회, 화면 크기 변경(`Ctrl + 휠` 확대/축소 등), `rerender`, `setTheme`, `makeSubTotal` 등 **시트를 다시 그리는 여러 동작**에서 발생하는 일반 이벤트입니다. 전체 발생 시점은 [onRenderFinish](/docs/events/on-render-finish)를 참고하세요. 단, `renderBody`(데이터 영역만 렌더링)로는 발생하지 않습니다. `onRenderFirstFinish`만 최초 생성 시 1회 발생합니다.

> **생성 시점 주의**: `create()`는 기본이 비동기(`sync: 0`)로 동작합니다.  
> 함수가 반환한 직후에는 시트가 아직 완성되지 않았을 수 있으므로, 생성 후 데이터 로드나 시트 조작은 [onRenderFirstFinish (event)](/docs/events/on-render-first-finish)에서 처리하고, 반드시 동기로 생성해야 한다면 `sync` 인자를 `1`로 지정합니다.  
> `create()`는 `Promise`가 아니라 **시트 객체를 반환**하므로 `await IBSheet.create(...)`로 감싸도 완료를 기다려 주지 않습니다. `async/await` 대신 위 방법(`onRenderFirstFinish` 또는 `sync: 1`)을 사용하세요.

```javascript
// 잘못된 예 — await를 붙여도 기다려 주지 않음
async function initSheet() {
  await IBSheet.create({ id: "sheet", el: "sheetDiv", options: OPT });
  sheet.doSearch("/search.do"); // 시트가 아직 준비되지 않아 오류
}
```

### Read More
 - [IBSheet.CommonOptions static](./common-options)
 - [IBSheet.onBeforeCreate static](./on-before-create)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.1.0.45|sync 기능 추가|
