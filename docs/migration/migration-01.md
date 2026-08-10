# 제품 파일 변경

<!-- synonyms: IBSheet7, 마이그레이션, sheet7, migration, v7, v8, ibsheet7에서 ibsheet8로, 제품 파일 변경, 파일 대응, ibsheet.js, ibsheet-common.js, ibsheet-dialog.js, 파일 구성, files, 라이선스 파일 -->

## 각 파일의 기능 비교

|IBSheet7 파일|기능|IBSheet8 파일|
|---|---|---|
|ibsheet.js|제품 core|ibsheet.js|
|ibleaders.js|라이선스|ibleaders.js|
|ibsheetinfo.js|초기화 상수, 함수|ibsheet-common.js|
|ibmsg|메세지 파일|ko.js, en.js|
|Main 폴더|css 파일 및 이미지|css/테마 폴더|
|ibsheet.cfg|공통 기능 속성|ibsheet-common.js|
|(없음)|찾기, 피벗 등 공통 다이얼로그|ibsheet-dialog.js|
|(없음)|파일 export/import 관련 모듈|ibsheet-excel.js|

IBSheet7에서는 화면에 `ibsheet.js`와 `ibsheetinfo.js` 두 파일만 include하면, 나머지 파일(`ibmsg`, `ibsheet.cfg`, `ibsheet.css`)은 ajax 통신으로 자동 로딩되었습니다.  
IBSheet8에서는 확장자가 없거나(`ibmsg`) 개별 확장자를 갖던(`ibsheet.cfg`) 파일이 모두 js 형태로 바뀌었고, 각 파일을 화면에 직접 include하는 방식으로 변경되었습니다.  
따라서 IBSheet8로 마이그레이션할 때는 아래 파일들을 추가해야 합니다.

## IBSheet8 사용 파일

**필수 파일**
1. `ibsheet.js` (IBSheet8 코어)
2. `/locale/ko.js` (또는 `en.js`) — 다국어 메세지 파일
3. `/css/default/main.css` (기본 디자인 css)

**선택 파일**
1. `ibsheet-common.js` (공통 기능 설정)
2. `ibsheet-dialog.js` (각종 다이얼로그 사용)
3. `ibsheet-excel.js` (엑셀/텍스트 다운로드/업로드)

## Example

```html
<!-- AS-IS (IBSheet7) -->
<script type="text/javascript" src="/common/sheet/js/ibsheet.js"></script>
<script type="text/javascript" src="/common/sheet/js/ibsheetinfo.js"></script>
```

```html
<!-- TO-BE (IBSheet8) -->
<!-- 필수 파일 -->
<link rel="stylesheet" href="/common/ibsheet8/css/default/main.css">
<script type="text/javascript" src="/common/ibsheet8/ibsheet.js"></script>
<script type="text/javascript" src="/common/ibsheet8/locale/ko.js"></script>

<!-- 선택 추가 파일 -->
<script type="text/javascript" src="/common/ibsheet8/ibsheet-common.js"></script>
<script type="text/javascript" src="/common/ibsheet8/ibsheet-dialog.js"></script>
<script type="text/javascript" src="/common/ibsheet8/ibsheet-excel.js"></script>
```

IBSheet8은 기본적으로 CSS3를 사용하므로 IE10 이상 브라우저에서 정상적으로 표시됩니다.

## Read More
- [파일 구성](/docs/intro/files)
