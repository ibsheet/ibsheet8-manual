# Head / Foot ***(appendix)***

<!-- synonyms: 헤드행, 풋행, 고정행, Head, Foot, 상단 고정행, 하단 고정행, 헤드 풋 추가, 커스텀 고정행 -->

> `Head`와 `Foot`은 시트에 고정되는 커스텀 행입니다.  
> `Head`는 **헤더와 데이터 영역 사이**, `Foot`은 **데이터 영역 아래**에 위치하며, 세로 스크롤해도 고정됩니다.  
> `Head`/`Foot` 행은 일반 데이터 행처럼 **열에 맞춰 셀이 배치**되고, 가로 스크롤 시 열과 함께 좌우로 움직입니다.   
> 열 구성과 무관하게 독립적인 셀 배치가 필요하면 [Solid](/docs/appx/solid)를 사용하세요.

## 생성 방법

### 1) 시트 생성 시 정적 생성 — `options.Head` / `options.Foot`

초기화 구문의 `Head` / `Foot` 배열에 행을 정의합니다.

```javascript
var OPT = {
    Cols: [
        { Header: "부서명", Name: "deptName", Type: "Text" },
        { Header: "1분기",  Name: "qt1",      Type: "Int" }
    ],
    // 상단 고정행 (헤더와 데이터 사이)
    Head: [
        {
            id: "HEAD1", CanEdit: 0, Color: "#EAF2FF",   // Kind 생략 (Head 배열이 종류를 정함)
            deptName: { Value: "상단 안내행", Align: "Center", Span: 2 }  // 2개 열 병합
        }
    ],
    // 하단 고정행 (데이터 아래) — 2개
    Foot: [
        {
            id: "FOOT1", CanEdit: 0, Color: "#F5F5F5",   // Kind 생략 (Foot 배열이 종류를 정함)
            deptName: { Value: "합계", Align: "Center" },
            qt1: { Type: "Int" }   // 값은 setValue 등으로 채움
        },
        {
            id: "FOOT2", CanEdit: 0,
            deptName: { Value: "평균", Align: "Center" },
            qt1: { Type: "Int" }
        }
    ]
};
```

아래는 `Foot` 커스텀 행(맨 아래 "2015년 자료" 행)이 데이터 영역 아래에 고정 표시된 예입니다.

![Foot 커스텀 행 예](/assets/imgs/foot.png "Foot 커스텀 행")

### 2) 시트 생성 후 동적 생성 — `showFixedRows`

[showFixedRows](/docs/funcs/core/show-fixed-rows)는 **행을 생성·표시**하는 함수입니다.   
함수는 행을 만들어줄 뿐이고, 그 행에 들어갈 **내용(셀 구성)** 은 아래 **행 구성**과 동일하게 지정합니다.   
`Kind`는 행의 **종류(역할)** 를 뜻하며([Kind appendix](/docs/appx/kind)), `Head`/`Foot`도 그 종류 값의 하나입니다.  
`options.Head`/`Foot` **배열**로 만들 땐 배열이 종류를 정하므로 `Kind`를 생략하지만, `showFixedRows`는 배열이 없어 각 객체에 **`Kind: "Head"` 또는 `Kind: "Foot"`** 로 종류를 지정합니다.

## 행 구성

각 `Head` / `Foot` 행은 다음으로 구성합니다.

|항목|설명|
|---|---|
|`id`|행의 고유 id. **생략하면 자동 부여**됩니다 (아래 *자동 `id` 번호* 참고). 특정 행을 참조하려면 직접 지정하세요.|
|`CanEdit`, `Color`, `CanFormula` 등|행 전체에 적용되는 **행 속성**(도움말 **Properties > Row**). 편집 가능 여부(`CanEdit`), 배경색(`Color`) 등을 지정합니다.<br/>셀에 `Formula`(아래 `컬럼명` 참고)를 걸어 자동 계산하려면 이 행에 **`CanFormula: 1`** 을 지정합니다.|
|`Def`|미리 정의한 **공통 설정 프리셋을 상속**합니다. `options.Def`에 임의 이름으로 프리셋을 만들고 `Def: "프리셋명"`으로 참조하면, 여러 `Head`/`Foot` 행에 같은 설정을 한 번에 적용할 수 있습니다.|
|`컬럼명`|`컬럼명`을 키로 주면 그 열 위치의 **셀**이 되며, **Cell 속성**(도움말 **Properties > Cell**)을 지정합니다 (`Value`, `Type`, `Align`, `Format`, `Span`, `Formula` 등).<br/>셀을 지정하지 않은 열은 **그 열을 `Cols`(열 정의)에 만들 때 준 속성**(`Type`, `Align`, `Format` 등)을 그대로 따릅니다.<br/>`Span`으로 여러 열을 병합합니다. (예: `Span: 2`)<br/>합계 등은 셀에 함수형 `Formula`(`function(fr){ ... fr.Sheet.getDataRows()... }`)를 걸어 자동 계산합니다(행에 `CanFormula: 1` 필요). → [Formula appendix](/docs/appx/formula)|

- **`Head`와 `Foot`은 기본값이 다릅니다** — `Head` 행은 `CanFocus`와 `CanEdit`가 기본 `1`(포커스와 편집 모두 가능), `Foot` 행은 기본 `0`(포커스와 편집 모두 불가). 바꾸려면 행에 해당 속성을 직접 지정합니다.
- 계산이 아니라 서버에서 받은 값 등을 넣을 때는 `onSearchFinish`에서 `setValue`로 직접 채웁니다.

### `Def` 프리셋으로 공통 설정

여러 `Head`/`Foot` 행에 같은 설정을 줄 때는 `options.Def`에 **임의 이름의 프리셋**을 만들고, 각 행에서 `Def: "프리셋명"`으로 상속합니다.

```javascript
var OPT = {
    Def: {
        // 임의 이름의 공통 프리셋 (여러 행에서 재사용)
        MyFoot: { CanEdit: 0, CanFocus: 0, Color: "#EFFFEF" }
    },
    Cols: [
        { Header: "항목", Name: "deptName", Type: "Text" },
        { Header: "수량", Name: "qty",      Type: "Int" }
    ],
    Foot: [
        { id: "FOOT_SUM", Def: "MyFoot", deptName: { Value: "합계", Align: "Center" }, qty: { Type: "Int" } },
        { id: "FOOT_AVG", Def: "MyFoot", deptName: { Value: "평균", Align: "Center" }, qty: { Type: "Int" } }
    ]
};
```

- `MyFoot`은 예약어가 아니라 **직접 붙인 이름**입니다. `Def.Row`(모든 행)와 `Def.Header`(헤더행)처럼 IBSheet이 정한 이름 외에, 이렇게 만든 이름도 행의 `Def`로 참조할 수 있습니다.

### `Formula`로 합계 `Foot` 만들기

`Foot` 셀에 **함수형 `Formula`** 를 걸면 데이터 행을 집계해 합계 등을 자동 표시할 수 있습니다. 계산을 쓰려면 **그 행에 `CanFormula: 1`** 을 지정합니다. (행에 직접 넣어도 되고, 모든 행에 적용하려면 `Def.Row`에 넣어도 됩니다.)

```javascript
var OPT = {
    Cols: [
        { Header: "항목", Name: "deptName", Type: "Text" },
        { Header: "수량", Name: "qty",      Type: "Int" }
    ],
    Foot: [
        {
            id: "FOOT_SUM", CanEdit: 0, CanFormula: 1,   // 이 행에서 계산 사용
            deptName: { Value: "합계", Align: "Center" },
            qty: { Type: "Int", Formula: sumQty }        // 함수형 Formula
        }
    ]
};

// qty 열의 데이터 합계
function sumQty(fr) {
    return fr.Sheet.getDataRows().reduce(function (acc, row) {
        return acc + fr.Sheet.getValue(row, "qty");
    }, 0);
}
```

### 자동 `id` 번호

`Head` 영역은 헤더행과 `HR#` 번호를 **공유**합니다. 첫 헤더행은 `Header`, 그다음 헤더행부터 `HR1`, `HR2`…를 차지하고, 커스텀 `Head` 행은 **헤더행 다음 번호**를 받습니다.

- 헤더행 1개(`Header`) → 커스텀 `Head` 행 = `HR1`
- 헤더행 2개(`Header`, `HR1`) → 커스텀 `Head` 행 = `HR2`
- 헤더행 3개(`Header`, `HR1`, `HR2`) → 커스텀 `Head` 행 = `HR3`

따라서 **헤더행 개수가 바뀌면 커스텀 `Head` 행의 자동 `id`도 밀립니다.** 특정 행을 안정적으로 참조하려면 `id`를 직접 지정하세요.  
`Foot`은 헤더와 무관하게 `FR1`, `FR2`… 순으로 붙습니다.

### Read More
- [showFixedRows method](/docs/funcs/core/show-fixed-rows)
- [Formula appendix](/docs/appx/formula)
- [Kind appendix](/docs/appx/kind)
- [시트 객체 기본 구조 getting started](/docs/start/basic-structure)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
