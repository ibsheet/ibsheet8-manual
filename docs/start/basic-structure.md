# 시트 객체 기본 구조

<!-- synonyms: 시트 객체 구조, 초기화 구문, options 구조, init structure, Def, Cfg, Cols, Events, Head, Foot, Solid, Filter -->

> `IBSheet.create`의 `options`(초기화 구문) 구조입니다.  
> 먼저 아래 **기본 구조**(자주 쓰는 핵심)를 익히고, `Def`, `Head`, `Foot`, `Solid`, `Filter` 등 나머지 항목이 필요하면 문서 아래 **상세 구조**를 참고하세요.

## 초기화 구문 구조 (기본)
```
options.(ROOT)
├── Def               // 각 영역의 공통 기능 설정
│   └── Row:{}        // 모든 데이터 행의 공통 기능 설정
│
├── Cfg:{}            // 시트 전역 기능 설정
│
├── LeftCols:[]       // 왼쪽 고정 영역 열 설정
├── Cols:[]           // 기본열 설정(가운데 영역)
├── RightCols:[]      // 우측 고정 영역 열 설정
│
└── Events:{}         // 이벤트 선언
```

|항목|설명|필수 여부|
|---|---|---|
|`Def`|행, 열, 헤더 등 **각 영역 전체에 한 번에 적용할 기본 속성**을 정의합니다. (예: `Def.Row.CanEdit = 0` → 모든 데이터 행 편집 불가)<br/>`Def.Row`에는 **Properties > Row**, `Def.Col`에는 **Properties > Col**의 속성을 지정합니다. (더 자세한 내용은 아래 **상세 구조** 참고)|선택|
|`Cfg`|시트 전체에 적용되는 설정 (예: 편집 불가 [CanEdit](/docs/props/cfg/can-edit), 정렬 허용 [CanSort](/docs/props/cfg/can-sort)).<br/>설정 가능한 전체 항목은 도움말 **Properties > Cfg**에서 확인|선택|
|`Cols`|가운데(메인) 영역의 열 목록. 열마다 `Name`(데이터 필드명)과 `Type`(열 종류)을 지정합니다.<br/>`Width`, `Align`, `Format` 등 도움말 **Properties > Col**의 속성을 함께 줄 수 있습니다. (`LeftCols` / `RightCols`도 동일)|**필수**|
|`LeftCols` / `RightCols`|왼쪽 / 오른쪽 **고정 열** 영역.<br/>가로 스크롤해도 자리를 지키는 고정 열로 **엑셀의 틀 고정**과 비슷합니다. 필요 없으면 생략 가능|선택|
|`Events`|시트 **전역(일반) 이벤트** 핸들러를 선언 (예: `onAfterClick`, `onAfterChange`). → [이벤트 사용법](/docs/events/01-event)|선택|

시트설정 예)
```javascript
var OPT =
{
    "Cfg": {                // 전역 기능 설정(cfg property)
        "CanEdit": 0,
    },
    "LeftCols": [           // 왼쪽영역(LeftSection) 고정 열 설정 (col property)
        { "Header": "NO", "Type": "Int", "Name": "SEQ", "Width": 50 },
        { "Header": "선택", "Type": "Bool", "CanEdit": 1, "Name": "CHK"} 
    ],
    "Cols": [               // 기본 열 설정(가운데영역)  (col property)
        { "Header": "부서명", "Name": "deptName", "Type": "Text", "Size": 30 }, 
        { "Header": "1분기", "Name": "qt1", "Type": "Int", "Width": 100, "Format": "#,##0 만원", "FormulaRow": "Avg" }, 
        { "Header": "2분기", "Name": "qt2", "Type": "Int", "Width": 100, "Format": "#,##0 만원", "FormulaRow": "Avg", "Color": "#EDEDED" }, 
        { "Header": "3분기", "Name": "qt3", "Type": "Int", "Width": 100, "Format": "#,##0 만원", "FormulaRow": "Avg" }, 
        { "Header": "4분기", "Name": "qt4", "Type": "Int", "Width": 100, "Format": "#,##0 만원", "FormulaRow": "Avg", "Color": "#EDEDED"}
    ],
    "RightCols": [],        // 오른쪽 영역(RightSection)
    "Events":{              // 이벤트 설정
        "onBeforeChange":function (evt) {
            ...
        }
    }
};
```

## 조회 데이터 구조
```js
var DATA = [
        {"deptName": "국내영업 1팀", "qt1": 15030, "qt2": 21102, "qt3": 20308, "qt4": 23041},
        {"deptName": "국내영업 2팀", "qt1": 25100, "qt2": 42460, "qt3": 38740, "qt4": 54765},
        {"deptName": "국내영업 3팀", "qt1": 11474, "qt2": 19671, "qt3": 24746, "qt4": 20754},
        {"deptName": "해외 영업팀", "qt1": 24146, "qt2": 24654, "qt3": 24164, "qt4": 48121}
    ]
```

## 시트 생성 구문
```js
IBSheet.create({
    "id": "mySheet", // 시트객체 이름 (SPA에서는 사용 X)
    "el": document.querySelector("div.part1 .gridarea"), // 시트를 생성할 html element 
    "options": OPT, // 초기화 구문
    "data": DATA  //초기 데이터
});
```

![로드된 시트 이미지](/assets/imgs/basicStructure.png "로드된 시트 이미지")

## 상세 구조

기본 구조 외에, 필요에 따라 사용하는 항목(`Def`, `Head`, `Foot`, `Solid`, `Filter` 등)까지 포함한 전체 구조입니다.

```
options.(ROOT)
├── Def               // 각 영역의 공통 기능 설정
│   ├── Row:{}        // 모든 데이터 행의 공통 기능 설정
│   ├── Col:{}        // 모든 데이터 열의 공통 기능 설정
│   ├── Header:{}     // 헤더 행의 공통 기능 설정
│   ├── CustomID:{}   // 임의의 행에 대한 설정
│   ├── Group: {}     // Group 행에 대한 설정
│   ├── SubSum : {}   // 소계/누계 행에 대한 설정
│   ├── FormulaRow:{} // FormulaRow행(합계)에 대한 설정
│   └── InfoRow:{}    // InfoRow(건수정보 행)에 대한 설정 (높이 등)
│
├── Cfg:{}            // 시트 전역 기능 설정
│
├── LeftCols:[]       // 왼쪽 고정 영역 열 설정
├── Cols:[]           // 기본열 설정(가운데 영역)
├── RightCols:[]      // 우측 고정 영역 열 설정
│
├── Events:{}         // 이벤트 선언
│
├── Head:[]           // 헤드영역에 커스텀행 추가/정의
├── Foot:[]           // 풋 영역에 커스텀행 추가/정의
├── Solid:[]          // Solid 행 추가/정의
└── Filter:{}         // 필터 행 추가/정의
```

|항목|설명|필수 여부|
|---|---|---|
|`Def`|행, 열, 헤더, 소계, 합계 등 **각 영역 전체에 한 번에 적용할 기본 속성**을 정의합니다. (예: `Def.Row.CanEdit = 0` → 모든 데이터 행 편집 불가)<br/>`Def.Row`와 `Def.Header`에는 도움말 **Properties > Row**, `Def.Col`에는 **Properties > Col**의 속성을 지정합니다.<br/>같은 속성을 개별 행/열에도 지정하면 개별 설정이 우선합니다.<br/>또한 다른 열을 계산해 보여주는 `Formula`(열 간 계산)를 쓰려면 `Def.Row`에 계산 사용 여부([CanFormula](/docs/props/row/can-formula))와 계산 순서([CalcOrder](/docs/props/row/calc-order))를 설정해야 해서 자주 사용됩니다.|선택|
|`Head` / `Foot`|헤더와 데이터 영역 사이(`Head`), 데이터 영역 아래(`Foot`)에 넣는 **고정 커스텀 행** → [Head / Foot appendix](/docs/appx/head-foot)|선택|
|`Solid`|시트 안에서 독립적인 기능을 수행하는 행 → [Solid appendix](/docs/appx/solid)|선택|
|`Filter`|헤더 아래에 **필터 행**을 정의합니다.<br/>열별로 필터 셀을 직접 구성할 수 있습니다 (아래 예제 참고).<br/>기본 필터 행만 켜려면 [ShowFilter (cfg)](/docs/props/cfg/show-filter).|선택|

시트설정 예)
```javascript
var OPT =
{
    "Def": {                                    // 각 영역 공통 설정
        "Row":    { "AlternateColor": "#FEEDFF" },      // 모든 데이터 행 공통
        "Col":    { "CanEdit": 0 },                      // 모든 열 공통
        "Header": { "Align": "Center", "TextStyle": 1 }, // 헤더행 공통
        "SubSum": { "Color": "#EEF3FB" }                 // 소계/누계 행 공통 (배경색 등 행 속성)
    },
    "Cfg": { "HeaderMerge": 3 },                // 전역 설정
    "LeftCols":  [ { "Header": "NO",    "Name": "SEQ",      "Type": "Int",  "Width": 50 } ],
    "Cols":      [ { "Header": "부서명", "Name": "deptName", "Type": "Text" } ],
    "RightCols": [ { "Header": "합계",   "Name": "total",    "Type": "Int" } ],
    "Head": [                                   // 상단 고정행 (헤더와 데이터 사이)
        { "id": "HEAD1", "CanEdit": 0, "deptName": "상단 고정 안내" }
    ],
    "Foot": [                                   // 하단 고정행 (데이터 아래)
        { "id": "FOOT1", "CanEdit": 0, "deptName": "합계", "total": { "Type": "Int" } }
    ],
    "Events": {                                     // 전역 이벤트
        "onAfterChange": function (evt) { /* ... */ }
    },
    "Solid": [                                  // Solid 행 (열 구성과 무관한 독립 행)
        {
            "id": "mySolidRow",
            "Space": 0,                 // 위치: -1~5 (0 = 헤더 위)
            "Height": 30,
            "Cells": "Msg",             // 셀 순서
            "Msg": { "Type": "Text", "Value": "고정 안내행", "CanEdit": 0 }
        }
    ],
    "Filter": {                                 // 필터 행 (헤더 아래) — 열별 필터 셀 구성
        "deptName": {
            "Button": "Defaults",               // 필터 셀에 목록 드롭다운 버튼
            "Defaults": "|*Rows"                // 조회된 값들을 체크리스트로 자동 구성 (*RowsVisible = 보이는 행만)
        }
    }
};
```

### Read More
- [Quick Start getting started](/docs/start/quick-start)
- [create static](/docs/static/create)
- [Header col](/docs/props/col/header)
- [ShowFilter cfg](/docs/props/cfg/show-filter)
- [Defaults col](/docs/props/col/defaults)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
