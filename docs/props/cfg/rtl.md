# Rtl ***(cfg)***

<!-- synonyms: RTL, right to left, 우측 정렬 모드, 우에서 좌, 아랍어, 히브리어, 페르시아어, 오른쪽에서 왼쪽, 우→좌, RTL 모드, 우측 방향, right-to-left, Arabic, Hebrew, RTL layout, mirror layout, 시트 반전, 좌우 반전 -->

> 시트 전체 레이아웃을 **우→좌(Right-to-Left) 방향으로 반전**하여, 아랍어·히브리어·페르시아어 등 RTL 언어권 사용자에게 적합한 화면으로 표시합니다.  
> 헤더/데이터 셀 배치, 스크롤 방향, 트리 들여쓰기, 소트/필터 아이콘 위치, 편집 다이얼로그 위치, 음수 기호(`-`) 위치 등이 모두 반전됩니다.  
> `exportData`/`down2Excel` 등 엑셀 다운로드 시에도 셀 정렬(`Align`)이 반전되어 저장되며, 서버 모듈(엑셀 서버 다운로드/업로드) 및 다이얼로그 플러그인(피벗·필터 등)도 RTL 모드로 동작합니다.  
> `제약사항`: RTL은 시트 생성 시점에 적용되어야 하며, 생성 이후 동적으로 켜고 끌 수는 없습니다.
>
> `필수 환경`: `ibsheet.js 8.4.0.18` / `ibsheet-dialog.js 1.0.53` / `ibsheet-excel.js 1.1.40` / `servermodule jar 2.1.7` **이상**의 파일을 사용해야 하며, **해당 버전에 맞는 CSS(테마)와 Locale 언어팩 파일**을 함께 적용해야 정상 동작합니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|기본 LTR(왼쪽→오른쪽) 레이아웃 (`default`)|
|`1(true)`|RTL(오른쪽→왼쪽) 레이아웃 사용|

### RTL 모드에서 반전되는 요소

|영역|반전 내용|
|---|---|
|셀 배치|첫 열이 화면 오른쪽부터 시작하도록 좌우 반전|
|스크롤|수평 스크롤 방향이 반전됨 (오른쪽 끝이 시작)|
|헤더 아이콘|정렬(Sort)·필터(Filter) 아이콘 위치가 좌↔우로 반전|
|셀 정렬|`Align:"Left"` 셀은 시각적으로 오른쪽에 배치|
|음수 기호|숫자 셀의 음수 기호(`-`)가 값의 오른쪽에 표시|
|트리 들여쓰기|트리 자식 노드의 들여쓰기가 오른쪽에서 왼쪽으로 확장|
|다이얼로그|편집·필터·피벗 등 다이얼로그의 열림 위치·방향 반전|
|엑셀 다운로드|`exportData`/`down2Excel` 시 `Align`이 반전되어 저장됨. 엑셀의 RTL 모드로 파일이 열림|

### Example
```javascript
// 시트 전체를 RTL 모드로 표시
options.Cfg = {
    Rtl: 1,
    MsgLocale: "Ar"   // 아랍어 언어팩과 함께 사용
};

options.Cols = [
    // Align 지정은 그대로 두어도 됩니다. RTL 모드가 시각적으로 반전합니다.
    {Type: "Text", Name: "Name",  Header: "이름", Align: "Left"},
    {Type: "Int",  Name: "Qty",   Header: "수량", Align: "Right"},
    {Type: "Date", Name: "Regdt", Header: "등록일"}
];
```

### Read More
- [MsgLocale cfg](/docs/props/cfg/msg-locale)
- [exportData method](/docs/funcs/core/export-data)
- [down2Excel method](/docs/funcs/excel/down-to-excel)

### Since

|product|version|desc|
|---|---|---|
|core|8.4.0.18|기능 추가|
|dialog|1.0.53|RTL 모드 지원 (필터·피벗 등 다이얼로그)|
|excel|1.1.40|RTL 모드 지원 (엑셀 다운로드 시 Align 반전)|
|servermodule|2.1.7|RTL 모드 지원 (서버 엑셀 다운로드/업로드)|
