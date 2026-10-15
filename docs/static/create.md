# create ***(static)***

<!-- synonyms: static, 정적 메소드, 전역 함수, static method, global function, IBSheet 정적, create, 시트 생성, IBSheet.create, 시트 인스턴스 생성, 시트 만들기, 그리드 생성, 시트 초기화, initialize, create sheet, 시트 안 보임, 시트 생성 안됨, Duplicate sheet_id, 시트 안 만들어짐, await 안됨, 생성 순서, 라이프사이클, SPA 시트 생성, 생성 후 조회, create 후 doSearch, 생성 완료 후 조회, 시트 준비 완료, onRenderFirstFinish, 생성 직후 조회 오류, 동적 컬럼, 컬럼 동적 생성, dynamic columns, dynamic header, 컬럼 메타데이터, 시트 재생성 -->

> 지정한 위치에 시트객체를 생성합니다.  
> 시트객체가 생성되면 `IBSheet` 객체에 배열 형식으로 추가(push)됩니다.

- `el` 객체의 크기에 따라 시트의 너비/높이가 결정됩니다.
- `el` 객체의 너비/높이가 정의되지 않은 경우에는 너비는 100%, 높이는 800px로 설정됩니다.
- 크기는 `el`의 **인라인 `style` 속성**으로 지정합니다. CSS 클래스로 지정한 크기를 쓰려면 [UseClassStyle](/docs/props/cfg/use_class-style)를 `1`로 설정합니다.
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
|id|`string`|<span class='required'>필수</span>|시트객체의 `id` (여기서 지정한 `id`는 `window` 객체에 `프로퍼티`로 생성됩니다.[전역변수])<br/>지정하는 것을 권장합니다. SPA처럼 고정 `id`를 쓰기 어려운 경우에는 생략할 수 있으며, 이때는 내부적으로 `id`가 자동 부여됩니다.|
|el|`mixed`( `string` \| `element` )|<span class='required'>필수</span>|시트객체가 생성될 대상 (해당 객체 안에 시트가 생성됨)<br/>`string`: div객체의 `id`<br/>`element`: `document.querySelector` 등으로 얻은 실제 DOM 요소 (`id` 전역변수를 피해야 하는 SPA 등에서 사용)|
|[options](/docs/start/basic-structure)|`object`|<span class='required'>필수</span>|초기화 정보를 갖고있는 `json 객체`|
|data|`array[object]`|<span class='optional'>선택</span>|생성과 동시에 로드 될 `데이터 배열`<br/>이 방식으로 넣으면 조회와 관련된 이벤트는 발생하지 않습니다.|
|sync|`boolean`|<span class='optional'>선택</span>|시트를 동기로 생성합니다<br/>`0(false)`:비동기 방식 (`default`)<br/>`1(true)`:동기 방식|

### Return Value
***object*** : 생성된 시트 객체

### Example

`create()`는 기본이 비동기라 호출 직후에는 시트가 아직 준비되지 않았습니다.  
생성 후 조회(`doSearch`, `loadSearchData`)나 시트 조작은 [onRenderFirstFinish](/docs/events/on-render-first-finish) 이벤트 안에서 합니다.  
화면에 시트가 여러 개이고 모두 생성된 뒤 실행하려면 [IBSheet.onRenderFirstFinishAll](/docs/static/on-render-first-finish-all)을 사용합니다.

```javascript
var opt = {
        //각 열에 대한 정의 (열의 이름, 유형(Type), 포맷(Format) 등을 설정)
        Cols:[
            {Header: {Value: "이름"}, Name: "sa_nm", Type: "Text"},
            {Header: {Value: "부서"}, Name: "sa_dept", Type: "Enum",
                Enum: "|경영지원|총무|인사", EnumKeys: "|01|02|03"},
            {Header: {Value: "입사일"}, Name: "sa_enterdate", Type: "Date", Width: 100, Format: "yyyy/MM/dd", DataFormat: "yyyyMMdd"}
        ],
        //생성이 끝난 뒤 서버에서 조회
        Events: {
            onRenderFirstFinish: function (evtParam) {
                evtParam.sheet.doSearch("./search.do");
            }
        }
    };

//시트객체 생성
IBSheet.create({
    id: "sheet", // 생성할 시트의 id
    el: "sheetDiv", // 시트를 생성할 Dom 객체 및 id
    options: opt // 생성될 시트의 속성
});
```

#### 그 밖의 생성 방법

```javascript
//el에 html element 설정
IBSheet.create({
    "id": "sheet", // 시트 id (window 전역변수로 등록됨, SPA에서는 id 충돌 주의)
    "el": document.querySelector("div.part1 .gridarea"), // el에 실제 DOM 요소를 직접 지정
    "options": opt // 초기화 구문
});

//SPA 등 고정 id를 쓰기 어려우면 id를 생략(자동 부여)하고 반환값으로 시트를 참조합니다.
//이벤트 콜백에서는 evtParam.sheet로 시트가 넘어오지만,
//이벤트 밖의 일반 함수에서 쓰려면 반환값을 접근 가능한 스코프(모듈/컴포넌트 필드 등)에 보관해야 합니다.
var mySheet; // 함수 밖(외부 스코프)에 선언, 지역 변수가 되지 않도록
function initSheet() {
    mySheet = IBSheet.create({
        el: document.querySelector("div.part1 .gridarea"), // el에 실제 DOM 요소를 직접 지정
        options: opt // 초기화 구문
    });
}
//이후 일반 함수에서 mySheet 로 접근 (조작은 생성 완료 후 = onRenderFirstFinish 이후)

//data 인자로 생성과 동시에 데이터 표시 (조회와 관련된 이벤트는 발생하지 않음)
var dataArr = [
    {sa_nm: "홍길동", sa_dept: "02", sa_enterdate: "19980305"},
    {sa_nm: "김한국", sa_dept: "01", sa_enterdate: "19890317"}
];
IBSheet.create({ id: "sheet", el: "sheetDiv", options: { Cols: opt.Cols }, data: dataArr });
```

#### 서버에서 받은 열 정의로 헤더를 동적으로 구성

서버에서 받은 열 정의(열 이름, 헤더, 타입, 너비 등)를 반복문으로 돌며 `Cols` 배열을 만들어 넘기면, 조회 결과에 따라 열 구성이 달라지는 시트를 만들 수 있습니다.

```javascript
// 서버에서 조회해 왔다고 가정한 열 정의
var columns = [
    { colId: "empNo",  colNm: "사번",   dataType: "Text", width: 100 },
    { colId: "hireDt", colNm: "입사일", dataType: "Date", width: 110, format: "yyyy-MM-dd", dataFormat: "yyyyMMdd" },
    { colId: "salary", colNm: "급여",   dataType: "Int",  width: 110, format: "#,##0" }
];

var cols = [];
for (var i = 0; i < columns.length; i++) {
    var c = columns[i];
    var col = { Name: c.colId, Header: c.colNm, Type: c.dataType, Width: c.width };
    if (c.format)     { col.Format = c.format; }
    if (c.dataFormat) { col.DataFormat = c.dataFormat; }
    cols.push(col);
}

// 같은 id 로 다시 만들 때는 기존 시트를 먼저 제거해야 합니다.
if (IBSheet.hasSheet("sheet")) { sheet.dispose(); }

IBSheet.create({
    id: "sheet",
    el: "sheetDiv",
    options: {
        Cols: cols,
        Events: {
            // 생성이 끝난 뒤 조회합니다. 조회 데이터의 키는 위 colId 와 같아야 합니다.
            onRenderFirstFinish: function (evtParam) {
                evtParam.sheet.doSearch("./search.do");
            }
        }
    }
});
```

> 서버에서 받은 이름을 열 이름(`Name`)으로 그대로 쓸 때는 [Name (col)](/docs/props/col/name)의 사용할 수 없는 이름에 해당하지 않는지 확인합니다.  
> 열 구성 전체가 바뀌면 위처럼 시트를 다시 만들고, 기존 시트에 열 몇 개만 추가할 때는 [addCol](/docs/funcs/core/add-col)을 사용합니다.

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
> 함수가 반환한 직후에는 시트가 아직 완성되지 않았으므로, 생성 후 데이터 로드나 시트 조작은 [onRenderFirstFinish (event)](/docs/events/on-render-first-finish)에서 처리합니다.  
> 반드시 동기로 생성해야 한다면 `sync` 인자를 `1`로 지정합니다.  
> `create()`는 `Promise`가 아니라 **시트 객체를 반환**하므로 `await IBSheet.create(...)`로 감싸도 완료를 기다려 주지 않습니다.  
> `async/await` 대신 위 방법(`onRenderFirstFinish` 또는 `sync: 1`)을 사용하세요.

```javascript
// 잘못된 예: await를 붙여도 기다려 주지 않음
async function initSheet() {
  await IBSheet.create({ id: "sheet", el: "sheetDiv", options: OPT });
  sheet.doSearch("./search.do"); // 시트가 아직 준비되지 않아 오류
}
```

올바른 방법은 위 **Example의 첫 번째 예제**를 참고합니다.

> **id 중복 주의**: `id`가 중복되면 `Can't creation : Duplicate sheet_id already exists` 경고가 발생하며 생성되지 않습니다.  
> SPA나 팝업처럼 고유한 `id`를 지정하기 어려우면, [IBSheet.hasSheet](./has-sheet)로 확인한 뒤 [dispose (method)](/docs/funcs/core/dispose) 또는 [IBSheet.disposeAll (static)](./dispose-all)로 제거하고 다시 생성하세요.

> **파일 로드 주의**: `ibsheet.js`, `main.css` 등 IBSheet 관련 파일은 한 페이지(DOM)당 1회만 로드합니다.  
> 특히 팝업 화면을 기존 DOM에 `append`하는 형태라면 팝업 쪽에서 이 파일들을 다시 호출하면 안 됩니다.  
> 재로드하면 전역 `IBSheet`가 재초기화되어 **이미 생성된 시트가 관리 목록(`IBSheet` 배열)에서 사라집니다.**

### Try it
- [Demo of create (서버에서 받은 열 정의로 헤더 구성)](https://jsfiddle.net/gh/get/library/pure/ibsheet/ibsheet8-manual-sample/tree/master/samples/method/addCol-DynamicCols/)

### Read More
- [IBSheet.CommonOptions static](./common-options)
- [IBSheet.onBeforeCreate static](./on-before-create)
- [시트객체 높이 설정 appendix](/docs/appx/sheet-height)
- [addCol method](/docs/funcs/core/add-col)
- [IBSheet.hasSheet static](./has-sheet)
- [dispose method](/docs/funcs/core/dispose)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.1.0.45|sync 기능 추가|
