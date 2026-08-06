# Quick Start

<!-- synonyms: 시작하기, 빠른 시작, 설치, 셋업, setup, getting started, 시트 생성, 첫 시트, 튜토리얼, 따라하기, 스크립트 로드, 파일 로드, import, ibsheet.js, ko.js, locale, 로케일, main.css, css 로드, ibleaders.js, 라이선스 파일, 로드 순서 -->

IBSheet8을 처음 접하는 개발자가 **아무 설정도 없는 상태에서 화면에 시트 하나를 띄우기까지**를 순서대로 따라할 수 있도록 정리한 문서입니다.  
각 단계를 위에서부터 그대로 따라오면 됩니다.

## STEP 0. 제품 파일 준비하기

IBSheet8은 자바스크립트 라이브러리라 별도의 설치 과정 없이, 배포 파일을 웹 경로에 복사해 사용합니다.

- 배포받은 `ibsheet` 폴더 전체를 웹 루트 아래 임의의 경로(예: `/ibsheet/`)에 복사합니다.
- 이때 `css` 폴더는 반드시 `ibsheet.js`와 **같은 경로**에 두어야 합니다. 경로가 다르면 화면 표시는 정상이지만 엑셀/PDF 다운로드 결과물에 디자인(스타일)이 적용되지 않습니다.
- 파일 종류와 폴더 구성은 [파일 구성](/docs/intro/files)을 참고하세요.

## STEP 1. HTML에 파일 추가하기

시트를 사용할 HTML 문서에 아래 파일을 추가합니다. **기본 모듈 4개는 필수**이고, 선택 모듈(`plugins`)은 필요한 기능만 골라 넣습니다.

```html
<!----- ibsheet 기본 모듈 ----->
<!-- 디자인 css -->
<link rel="stylesheet" type="text/css" href="ibsheet/css/default/main.css">
<!-- 시트 코어 파일 -->
<script src="ibsheet/ibsheet.js"></script>
<!-- 라이선스 파일 -->
<script src="ibsheet/ibleaders.js"></script>
<!-- 메세지 파일 ko.js 나 en.js 중 하나 추가 -->
<script src="ibsheet/locale/ko.js"></script>


<!----- ibsheet 선택 모듈 ----->
<!-- 엑셀 다운/업로드 관련 모듈 -->
<script src="ibsheet/plugins/ibsheet-excel.js"></script>
<!-- 찾기,상세보기 등 다이얼로그 관련 모듈 -->
<script src="ibsheet/plugins/ibsheet-dialog.js"></script>
<!-- 공통 속성 관련 모듈 -->
<script src="ibsheet/plugins/ibsheet-common.js"></script>
```

- **위치**: 시트를 생성·사용하는 스크립트보다 **먼저 로드**되도록 추가합니다(보통 `<head>` 안).
- **순서**: 기본 모듈을 먼저, 선택 모듈(`plugins`)을 그 뒤에 둡니다. `plugins`의 파일(`ibsheet-excel.js` 등)은 반드시 `ibsheet.js` 이후에 include해야 합니다.

## STEP 2. 시트를 그릴 영역(div) 만들기

시트는 단독으로 생성할 수 없습니다. 먼저 시트를 그릴 `div` 요소를 만들고, 그 `div`의 `id`를 시트 생성 시 `el` 값으로 지정하면 해당 `div` 안에 시트가 그려집니다.

```html
<!-- 시트가 될 DIV 객체 -->
<div id="sheetDiv" style="width:100%; height:500px;"></div>
```

- 시트의 너비·높이는 이 `div`의 크기를 따릅니다. **`div`에 높이가 없으면 너비는 100%, 높이는 800px**가 기본값으로 적용됩니다.
- 높이를 `100%` 등 상대값으로 줄 때는 **부모 요소의 높이가 고정**되어 있어야 합니다. 창 크기에 맞춰 시트가 늘고 줄어드는 반응형 레이아웃은 [시트객체 높이 설정](/docs/appx/sheet-height)을 참고하세요.
- 시트 높이는 고정된 행(헤더·필터·합계 행 등)이 모두 보일 정도(보통 150~200px 이상)로 설정해야 하며, 이보다 작으면 시트가 생성되지 않을 수 있습니다.

## STEP 3. 열(Cols) 정의하기

시트에 어떤 열을 보여줄지 `options`의 `Cols`에 정의합니다. 각 열에는 **`Name`(데이터 필드명)과 `Type`(열 종류)을 반드시** 지정합니다.

```javascript
var OPT = {
    //각 열에 대한 정의 (열의 이름, 유형(Type), 포맷(Format) 등을 설정)
    Cols: [
        { Header: "이름",     Name: "sa_nm",        Type: "Text" },
        { Header: "사원번호", Name: "sa_id",        Type: "Text", Align: "center" },
        { Header: "부서",     Name: "sa_dept",      Type: "Enum",
          Enum: "|경영지원|총무|인사|설계|시공1|시공2", EnumKeys: "|01|02|03|04|05|06" },
        { Header: "직급",     Name: "sa_position",  Type: "Enum",
          Enum: "|대표|상무|이사|부장|차장|과장|대리|사원", EnumKeys: "|A1|A2|A3|B0|B1|C4|C5|C6" },
        { Header: "입사일",   Name: "sa_enterdate", Type: "Date", Width: 100, Format: "yyyy/MM/dd" },
        { Header: "비고",     Name: "sa_desc",      Type: "Lines" }
    ]
};
```

- 두 줄 이상의 헤더를 만들거나 헤더 안에서 셀을 병합하려면 [(col)Header](/docs/props/col/header) 속성을 참고하세요.

## STEP 4. 시트 생성하기 (IBSheet.create)

STEP 2의 `div`와 STEP 3의 `options`를 [IBSheet.create()](/docs/static/create)에 넘기면 시트가 생성됩니다.  
`el`에는 STEP 2에서 만든 `div`의 `id`를 지정합니다.

STEP 1~4를 하나로 합친 전체 HTML은 다음과 같습니다.  
이 파일을 그대로 저장해 브라우저에서 열면 시트가 생성됩니다.

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <!-- STEP 1. ibsheet 파일 추가 -->
  <link rel="stylesheet" type="text/css" href="ibsheet/css/default/main.css">
  <script src="ibsheet/ibsheet.js"></script>
  <script src="ibsheet/ibleaders.js"></script>
  <script src="ibsheet/locale/ko.js"></script>

  <script>
    // STEP 3~4. 열 정의 + 시트 생성
    function initSheet() {
      var OPT = {
        Cols: [
          { Header: "이름",     Name: "sa_nm",        Type: "Text" },
          { Header: "사원번호", Name: "sa_id",        Type: "Text", Align: "center" },
          { Header: "부서",     Name: "sa_dept",      Type: "Enum",
            Enum: "|경영지원|총무|인사|설계|시공1|시공2", EnumKeys: "|01|02|03|04|05|06" },
          { Header: "직급",     Name: "sa_position",  Type: "Enum",
            Enum: "|대표|상무|이사|부장|차장|과장|대리|사원", EnumKeys: "|A1|A2|A3|B0|B1|C4|C5|C6" },
          { Header: "입사일",   Name: "sa_enterdate", Type: "Date", Width: 100, Format: "yyyy/MM/dd" },
          { Header: "비고",     Name: "sa_desc",      Type: "Lines" }
        ]
      };
      
      IBSheet.create({
        id: "sheet",     // 생성할 시트의 id
        el: "sheetDiv",  // STEP 2에서 만든 div의 id
        options: OPT     // 초기화 구문
      });
    }

    // DOM 로딩이 끝난 뒤 시트 생성
    document.addEventListener("DOMContentLoaded", initSheet);
  </script>
</head>
<body>
  <!-- STEP 2. 시트를 그릴 div -->
  <div id="sheetDiv" style="width:100%; height:500px;"></div>
</body>
</html>
```

![시트생성](/assets/imgs/quickStart2.png "열 설정이 적용된 ibsheet")
[그림] 열 설정이 적용된 시트

## STEP 5. 데이터 로드하기

시트에 데이터를 채우는 표준 방법은 **조회 함수**입니다. 이미 받아둔 json은 [loadSearchData()](/docs/funcs/core/load-search-data), 서버 url 호출은 [doSearch()](/docs/funcs/core/do-search)를 사용합니다.

```javascript
// 이미 받아둔 json 데이터를 로드
sheet.loadSearchData(rtnData);

// url을 호출해 데이터를 로드
sheet.doSearch("/ex/getPersonData.do", "edate=19950101&position=C1");
```

![시트생성](/assets/imgs/quickStart3.png "데이터가 로드된 ibsheet")
[그림] 데이터가 로드된 시트

> **비동기 주의**: `IBSheet.create()`와 조회 함수(`loadSearchData`/`doSearch`)는 비동기로 동작합니다.  
> 생성 직후 시트 함수를 바로 호출하면 시트가 아직 완성되지 않아 오류가 날 수 있습니다.  
> 생성 후 실행할 로직(예: 조회)은 [onRenderFirstFinish](/docs/events/on-render-first-finish) 이벤트에 넣습니다.  
> 화면에 시트가 여러 개이고 **모두 준비된 뒤** 실행하려면 [IBSheet.onRenderFirstFinishAll](/docs/static/on-render-first-finish-all) 정적 콜백을 사용합니다.  
> 이벤트는 `options.Events`에 등록하고, 콜백 안에서 시트 객체는 `evtParam.sheet`로 참조합니다.

```javascript
var OPT = {
    Cols: [ /* ... */ ],
    Events: {
        onRenderFirstFinish: function (evtParam) {
            // 시트가 완성된 후 조회
            evtParam.sheet.doSearch("/ex/getPersonData.do");
        }
    }
};
```

`IBSheet.create`의 `data` 인자로도 생성과 동시에 데이터를 넣을 수 있지만 **권장하지 않습니다.** 실제 개발에서는 위처럼 조회 함수(`loadSearchData` / `doSearch`)로 데이터를 불러옵니다.

```javascript
// 권장하지 않음 — data 인자로 로드
var DATA = [
    { sa_nm: "홍길동", sa_id: "9821450", sa_dept: "04", sa_position: "B0", sa_enterdate: "19980305", sa_desc: "" },
    { sa_nm: "김한국", sa_id: "9510427", sa_dept: "01", sa_position: "A3", sa_enterdate: "19890317", sa_desc: "" }
];

IBSheet.create({ id: "sheet", el: "sheetDiv", options: OPT, data: DATA });
```

## STEP 6. 시트가 안 보일 때 점검

- 개발자도구(F12) → 네트워크 탭에서 STEP 1에서 추가한 파일들이 모두 **200**으로 로드됐는지 확인합니다.
- 시트가 보이지 않으면 다음을 점검하세요.
  - STEP 2의 `div`가 실제로 존재하고, `el` 값과 `div`의 `id`가 일치하는가
  - 파일 경로가 맞는가 (특히 `css` 폴더가 `ibsheet.js`와 같은 경로인가)
  - 로드 순서가 맞는가 (`plugins`가 `ibsheet.js` 뒤인가)
  - `div` 높이가 너무 작지 않은가 (고정 행이 표시될 최소 높이가 필요)

## STEP 7. 자주 쓰는 기능 맛보기

여기까지 하면 화면에 시트가 뜹니다. 이제 자주 쓰는 기본 기능을 살펴봅니다.

### 행 추가

[addRow()](/docs/funcs/core/add-row) 함수로 신규 행을 추가합니다.

```javascript
// 선택 행 위로 새 행을 추가
sheet.addRow(sheet.getFocusedRow(), 1);
```

### 셀 값 확인 / 변경

[getValue](/docs/funcs/core/get-value) / [setValue](/docs/funcs/core/set-value)로 셀 값을 읽거나 바꿉니다.

```javascript
// 셀 값 읽기 — 첫 데이터 행의 "sa_nm" 값
var name = sheet.getValue(sheet.getFirstRow(), "sa_nm");

// 셀 값 쓰기 — 100번째 행의 "sa_desc" 변경
sheet.setValue(sheet.getRowByIndex(100), "sa_desc", "임계값 근접 경고!");
```

### 글자색 / 배경색 설정

[setAttribute()](/docs/funcs/core/set-attribute)로 특정 셀의 속성을 변경합니다.

```javascript
// "sa_id" 컬럼의 배경색을 변경
sheet.setAttribute(null, "sa_id", "Color", "#FF0000");

// 마지막 행의 글자색을 변경
sheet.setAttribute(sheet.getLastRow(), null, "TextColor", "#0000FF");
```

### 수정된 데이터 추출 / 저장

[getSaveJson()](/docs/funcs/core/get-save-json)으로 수정·추가·삭제된 행을 행 단위 json으로 추출합니다.

```javascript
var chgData = sheet.getSaveJson();
```

```javascript
{
    "data": [
        // 삭제 데이터
        { "id": "AR2", "sa_nm": "...", "STATUS": "Deleted" },
        // 신규 데이터
        { "id": "AR51", "sa_nm": "...", "STATUS": "Added" },
        // 수정 데이터
        { "id": "AR5", "sa_nm": "...", "STATUS": "Changed" }
    ]
}
```

수정 여부는 [hasChangedData()](/docs/funcs/core/has-changed-data)로 확인하고, 서버로 저장·반영까지 한 번에 처리하려면 [doSave()](/docs/funcs/core/do-save)를 사용합니다.

### 행 삭제

```javascript
// 특정 행을 즉시 삭제
sheet.removeRow(sheet.getFirstRow());
```

[deleteRow()](/docs/funcs/core/delete-row)는 행 상태를 `Deleted`로 바꾸고(저장 시 서버 전송), [removeRow()](/docs/funcs/core/remove-row)는 시트에서 즉시 제거합니다.

## STEP 8. 다음 단계 (더 배우기)

기본 시트를 띄웠다면, 아래 문서로 각 기능을 더 자세히 익힐 수 있습니다.

- 전체 흐름을 순서대로 배우려면 → [기초 개발자 교육](/docs/appx/basic-course)
- 메소드 호출 기초(파라미터 넘기는 법) → [method 사용법 기초](/docs/funcs/method)
- 이벤트 사용법 → [event 사용법](/docs/events/01-event)
- 초기화 옵션(`options`) 기본 구조 → [시트 객체 기본 구조](/docs/start/basic-structure)
- 조회 방식(SearchMode)별 동작 → [SearchMode](/docs/props/cfg/search-mode)

### Read More
- [파일 구성 introduction](/docs/intro/files)
- [create static](/docs/static/create)
- [시트객체 높이 설정 appendix](/docs/appx/sheet-height)
- [기초 개발자 교육 appendix](/docs/appx/basic-course)
- [시트 객체 기본 구조 getting started](/docs/start/basic-structure)
- [Header col](/docs/props/col/header)
- [method 사용법 기초 method](/docs/funcs/method)
- [event 사용법 기초 event](/docs/events/01-event)
- [onRenderFirstFinish event](/docs/events/on-render-first-finish)
- [loadSearchData method](/docs/funcs/core/load-search-data)
- [doSearch method](/docs/funcs/core/do-search)
- [getSaveJson method](/docs/funcs/core/get-save-json)
- [doSave method](/docs/funcs/core/do-save)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
