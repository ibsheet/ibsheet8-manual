# Dialog Templates ***(appendix)***

<!-- synonyms: 다이얼로그 템플릿, dlgTemplates, dialog template, 다이얼로그 커스터마이징, 다이얼로그 디자인 변경, DialogTemplatePath, 템플릿 폴더, 다이얼로그 배포 -->

> `ibsheet-dialog.js` 플러그인 다이얼로그는 HTML/CSS를 `dlgTemplates/` 폴더의 템플릿 파일로 제공합니다.  
> 이 문서는 템플릿 파일의 배포와 커스터마이징 방법을 설명합니다.

## 개요

`showFindDialog`, `showEditDialog`, `showDownloadDialog` 등 **플러그인 다이얼로그**는 `ibsheet-dialog.js` 안에 HTML/CSS가 하드코딩되어 있었습니다.  
`ibsheet-dialog` **1.0.46** 버전부터 이 하드코딩을 걷어내고, `dlgTemplates/` 폴더의 **HTML/CSS 파일**로 제공하도록 변경되었습니다.  
템플릿 파일을 직접 수정하면 다이얼로그의 구조와 디자인을 커스터마이징할 수 있습니다.

## 배포 (필수)

`ibsheet-dialog.js`와 **`dlgTemplates/` 폴더를 함께 배포**해야 합니다.  
템플릿 파일을 찾지 못하면 해당 다이얼로그가 정상적으로 열리지 않습니다.

> **하위 호환**: 1.0.46 미만 버전은 HTML/CSS가 스크립트 파일에 포함되어 있어 `dlgTemplates/` 폴더 없이도 동작합니다.  
> 1.0.46 이상으로 올릴 때는 `dlgTemplates/` 폴더를 함께 배포해야 하며, 빠뜨리면 다이얼로그가 열리지 않습니다.

## 템플릿 경로 설정

`ibsheet-dialog.js`와 `dlgTemplates/`를 같은 폴더에 두면 별도 설정 없이 동작합니다(스크립트 위치를 기준으로 자동 감지).  
폴더 위치가 다르면 `DialogTemplatePath`로 경로를 지정할 수 있습니다.

템플릿 폴더 경로는 아래 순서로 결정됩니다.

1. `IBSheet.CommonOptions.Cfg.DialogTemplatePath` — [IBSheet.CommonOptions](/docs/static/common-options)의 `Cfg`에 설정
2. `IBSheet.DialogTemplatePath` — 전역에 직접 설정
3. `DialogTemplatePath`가 없으면 `ibsheet-dialog.js` 스크립트가 위치한 경로의 `dlgTemplates/` 폴더에서 자동 감지

```javascript
// IBSheet.CommonOptions.Cfg 에 지정 (스크립트와 다른 위치를 가리킴)
IBSheet.CommonOptions = {
  Cfg: {
    DialogTemplatePath: "/assets/custom/dialogTemplates/"
  }
};

// 또는 전역에 직접 지정
IBSheet.DialogTemplatePath = "/assets/custom/dialogTemplates/";
```

## 커스터마이징

각 다이얼로그는 `HTML` 파일과 `CSS` 파일 한 쌍으로 구성됩니다. 파일을 직접 수정해 구조와 디자인을 변경할 수 있습니다.

- **HTML**: `<!-- [SECTION] --> … <!-- [/SECTION] -->` 형식의 섹션(예: `HEAD`, `BODY`)으로 구성됩니다. 클래스, 스타일, 배치는 자유롭게 변경할 수 있으나 각 템플릿 파일 주석의 **"필수 요소" id는 그대로 유지**해야 동작합니다.
- **`{{placeholder}}`**: 다이얼로그를 만들 때 자동으로 치환되는 값입니다(예: `{{sheetId}}`, `{{prefix}}`, `{{lang_FindNext}}`). 각 템플릿 파일 상단 주석에 사용 가능한 placeholder가 정리되어 있습니다.
- **CSS**: 해당 다이얼로그의 스타일을 정의합니다. `{{prefix}}`는 시트의 테마 접두사([Style (cfg)](/docs/props/cfg/style) 또는 [setTheme (method)](/docs/funcs/core/set-theme)로 결정)에 따라 치환됩니다. 설정하지 않으면 기본 테마(`css/default/main.css`)의 접두사 `IB`가 사용됩니다.

각 템플릿 파일 상단 주석에 사용 가능한 placeholder, 필수 요소 id, 섹션 구성이 정리되어 있으니 자세한 내용은 해당 주석을 참고하세요.

## 템플릿 파일

`dlgTemplates/` 폴더에는 다이얼로그별 HTML/CSS 파일이 있습니다.

|파일|관련 함수|
|---|---|
|`findDialog`|[showFindDialog](/docs/funcs/dialog/show-find-dialog)|
|`editDialog`|[showEditDialog](/docs/funcs/dialog/show-edit-dialog)|
|`htmlEditDialog`|[showHtmlEditDialog](/docs/funcs/dialog/show-html-edit-dialog)|
|`sortDialog`|[showSortDialog](/docs/funcs/dialog/show-sort-dialog)|
|`downloadDialog`|[showDownloadDialog](/docs/funcs/dialog/show-download-dialog)|
|`uploadDialog`|[showUploadDialog](/docs/funcs/dialog/show-upload-dialog)|
|`chartDialog`|[showChartDialog](/docs/funcs/dialog/show-chart-dialog)|
|`pivotDialog`|[showPivotDialog](/docs/funcs/dialog/show-pivot-dialog)|
