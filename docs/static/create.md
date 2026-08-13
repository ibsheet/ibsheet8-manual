# create ***(static)***

<!-- synonyms: static, 정적 메소드, 전역 함수, static method, global function, IBSheet 정적, create, 시트 생성, IBSheet.create, 시트 인스턴스 생성, 시트 만들기, 그리드 생성, 시트 초기화, initialize, create sheet, 시트 안 보임, 시트 생성 안됨, Duplicate sheet_id, 시트 안 만들어짐, await 안됨, 생성 순서, 라이프사이클, SPA 시트 생성 -->

> 지정한 위치에 시트객체를 생성합니다.<br/>
> 시트객체가 생성되면 `IBSheet`객체에 배열형식으로 추가(push)됩니다.<br/>

> 지정한 위치에 시트객체를 생성합니다.  
> 시트객체가 생성되면 `IBSheet` 객체에 배열 형식으로 추가(push)됩니다.

- `el` 객체의 크기에 따라 시트의 너비/높이가 결정됩니다.
- `el` 객체의 너비/높이가 정의되지 않은 경우에는 너비는 100%, 높이는 800px로 설정됩니다.
- 화면 크기에 맞춘 높이 지정(반응형)은 [시트객체 높이 설정](/docs/appx/sheet-height)을 참고하세요.

### Syntax
```javascript
// 위치 인자 방식
object IBSheet.create(id, el, options, data, sync);

// 옵션 객체 방식 (아래 예제 참고)
object IBSheet.create({ id, el, options, data, sync });
```

### Parameters
|Name|Type|Required|Description|
|----------|-----|---|----|
|id|`string`|<span class='required'>필수</span>|시트객체의 `id` (여기서 지정한 `id`는 `window` 객체에 `프로퍼티`로 생성됩니다.[전역변수])<br/>생략하면 내부적으로 `id`가 자동 부여됩니다.|
|el|`mixed`( `string` \| `element` )|<span class='required'>필수</span>|시트객체가 생성될 대상 (해당 객체 안에 시트가 생성됨)<br/>`string`: div객체의 `id`<br/>`element`: `document.querySelector` 등으로 얻은 실제 DOM 요소 (`id` 전역변수를 피해야 하는 SPA 등에서 사용)|
|[options](/docs/start/basic-structure)|`object`|<span class='required'>필수</span>|초기화 정보를 갖고있는 `json 객체`|
|data|`array[object]`|<span class='optional'>선택</span>|생성과 동시에 로드 될 `데이터 배열`|
|sync|`boolean`|<span class='optional'>선택</span>|시트를 동기로 생성합니다<br/>`0(false)`:비동기 방식 (`default`)<br/>`1(true)`:동기 방식|

### Return Value
***object*** : 생성된 시트 객체

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
    sync: 1 // 1: 동기 방식으로 생성 (0 또는 생략 시 비동기)
});

//el에 html element 설정
IBSheet.create({
    "id": "sheet",  // 시트 id (window 전역변수로 등록됨, SPA에서는 id 충돌 주의)
    "el": document.querySelector("div.part1 .gridarea"),  // el에 실제 DOM 요소를 직접 지정
    "options": opt, // 초기화 구문
    "data": dataArr // 초기 데이터
});

//SPA 등 고정 id를 쓰기 어려우면 id를 생략(자동 부여)하고 반환값으로 시트를 참조합니다.
//이벤트 콜백에서는 evtParam.sheet로 시트가 넘어오지만,
//이벤트 밖의 일반 함수에서 쓰려면 반환값을 접근 가능한 스코프(모듈/컴포넌트 필드 등)에 보관해야 합니다.
var mySheet;                       // 함수 밖(외부 스코프)에 선언, 지역 변수가 되지 않도록
function initSheet() {
    mySheet = IBSheet.create({
        el: document.querySelector("div.part1 .gridarea"),  // el에 실제 DOM 요소를 직접 지정
        options: opt                                         // 초기화 구문
    });
}
//이후 일반 함수에서 mySheet 로 접근 (조작은 생성 완료 후)
```
### 생성 흐름 (라이프사이클)

`IBSheet.create()`를 호출하면 아래 순서로 시트가 만들어집니다.

1. `IBSheet.create()` 호출
2. [IBSheet.CommonOptions (static)](./common-options)와 호출 시 전달한 `options`가 머지됨
3. [IBSheet.onBeforeCreate (static)](./on-before-create) 훅이 정의되어 있으면 실행되어 머지된 옵션을 최종 수정 (반드시 수정된 객체를 `return`)
4. 시트 객체 생성 및 최초 렌더링
5. [onRenderFirstFinish (event)](/docs/events/on-render-first-finish) 발생 (최초 1회), 이 시점부터 시트를 사용할 수 있음

생성 과정에서 발생하는 렌더 이벤트 순서는 다음과 같습니다.

|순서|이벤트|설명|
|---|---|---|
|1|`onRenderStart`|시트를 렌더링하기 전에 발생|
|2|`onRenderFinish`|시트가 렌더링된 후 발생|
|3|[onRenderFirstFinish](/docs/events/on-render-first-finish)|시트가 처음 생성되어 렌더링될 때 발생 (최초 1회만)|

`onRenderStart`와 `onRenderFinish`는 생성뿐 아니라 조회, 화면 크기 변경(`Ctrl + 휠` 확대/축소 등), `rerender`, `setTheme`, `makeSubTotal` 등 **시트를 다시 그리는 여러 동작**에서 발생하는 일반 이벤트입니다.  
전체 발생 시점은 [onRenderFinish](/docs/events/on-render-finish)를 참고하세요.  
단, `renderBody`(데이터 영역만 렌더링)로는 발생하지 않습니다.  
`onRenderFirstFinish`만 최초 생성 시 1회 발생합니다.

### 주의 사항

> **생성 시점 주의**: `create()`는 기본이 비동기(`sync: 0`)로 동작합니다.  
> 함수가 반환한 직후에는 시트가 아직 완성되지 않았을 수 있으므로, 생성 후 데이터 로드나 시트 조작은 [onRenderFirstFinish (event)](/docs/events/on-render-first-finish)에서 처리합니다.  
> 반드시 동기로 생성해야 한다면 `sync` 인자를 `1`로 지정합니다.  
> `create()`는 `Promise`가 아니라 **시트 객체를 반환**하므로 `await IBSheet.create(...)`로 감싸도 완료를 기다려 주지 않습니다.  
> `async/await` 대신 위 방법(`onRenderFirstFinish` 또는 `sync: 1`)을 사용하세요.

```javascript
// 잘못된 예: await를 붙여도 기다려 주지 않음
async function initSheet() {
  await IBSheet.create({ id: "sheet", el: "sheetDiv", options: OPT });
  sheet.doSearch("/search.do"); // 시트가 아직 준비되지 않아 오류
}
```

> **id 중복 주의**: `id`가 중복되면 `Can't creation : Duplicate sheet_id already exists` 경고가 발생하며 생성되지 않습니다.  
> SPA나 팝업처럼 UNIQ한 `id`를 지정하기 어려우면, [IBSheet.hasSheet](./has-sheet)로 확인한 뒤 [dispose (method)](/docs/funcs/core/dispose) 또는 [IBSheet.disposeAll (static)](./dispose-all)로 제거하고 다시 생성하세요.

> **파일 로드 주의**: `ibsheet.js`, `main.css` 등 IBSheet 관련 파일은 한 페이지(DOM)당 1회만 로드합니다.  
> 특히 팝업 화면을 기존 DOM에 `append`하는 형태라면 팝업 쪽에서 이 파일들을 다시 호출하면 안 됩니다.  
> 재로드하면 전역 `IBSheet`가 재초기화되어 **이미 생성된 시트가 관리 목록(`IBSheet` 배열)에서 사라집니다.**

### Read More
 - [IBSheet.CommonOptions static](./common-options)
 - [IBSheet.onBeforeCreate static](./on-before-create)
 - [시트객체 높이 설정 appendix](/docs/appx/sheet-height)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.1.0.45|sync 기능 추가|
