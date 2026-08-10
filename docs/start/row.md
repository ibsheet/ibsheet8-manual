# 행(Row) 구조에 대한 이해

<!-- synonyms: 시작하기, getting started, 빠른 시작, 시작, ibsheet 시작, 행 구조, row 구조, 행 정의, Data 배열, 데이터 행 -->

> 시트를 가로로 나눠 보면 크게 **상단 고정 / 가운데(데이터) / 하단 고정** 세 부분으로 나뉩니다.  
> **가운데**는 스크롤되는 데이터 영역입니다. **상단 고정**은 데이터 영역 위, **하단 고정**은 데이터 영역 아래에 고정되어 세로 스크롤해도 항상 보입니다.  
> 각 부분에 어떤 행이 있는지는 아래에서 설명합니다. 행의 종류(Kind)는 [Kind appendix](/docs/appx/kind)를 참고하세요.

---
## 상단 고정

데이터 영역 위에 고정되어 항상 보이는 부분입니다. 다음 행들이 포함됩니다.

- **헤더행** — 열 제목을 보여주고, 클릭 시 소팅, 열 이동, 너비 조절을 합니다.
- **필터행** — 열별로 조건을 입력해 데이터를 거릅니다.
- **커스텀 행(`Head`)** — 헤더행 아래에 고정으로 넣는 행입니다.

### *헤더행*
시트 생성시 `options.Cols.Header`를 통해 설정한 값들이 헤더에 들어가게 됩니다.  
헤더 셀은 클릭시 소팅이 되거나 드래그를 통해 열의 위치이동, 컬럼의 사이즈 조절 등의 역할을 수행합니다.

```javascript
var options = {
    "Cols": [
        {
            Header: [
                {    // 열의 헤더 설정 개별 셀 설정
                    "Value": "부서정보",
                    "Color": "#085820",
                    "Span": 2
                }, "부서명"
            ],
            "Name": "deptName", "Type": "Text", "Size": 100
        }, {
            Header: ["", "부서코드"],
            "Name": "deptCd", "Type": "Text", "Width": 100
        }, {
            Header: [
                {
                    "Value": "2014 년 실적",
                    "Color": "#6699FF",
                    "Span": 4
                }, "1분기"
            ],
            "Name": "qt1", "Type": "Int", "Width": 100
        }, {
            Header: ["", "2분기"],
            "Name": "qt2", "Type": "Int", "Width": 100
        }, {
            Header: ["", "3분기"],
            "Name": "qt3", "Type": "Int", "Width": 100
        }, {
            Header: ["", "4분기"],
            "Name": "qt4", "Type": "Int", "Width": 100
        }
    ]
};
```
![해더행](/assets/imgs/header1.png "헤더행")  
[생성된 헤더행]

### *필터행*
(`cfg`) [ShowFilter](/docs/props/cfg/show-filter)나 sheet.[showFilterRow()](/docs/funcs/core/show-filter-row)함수를 통해 생성되는 필터행도 상단 고정 영역에 위치합니다.
```javascript
sheet.showFilterRow();
```
![필터행](/assets/imgs/header2.png "필터행")  
[필터행]

### *커스텀 행(Head)*
`options.Head`에 정의해 **헤더행 아래**(필터행이 있으면 그 아래)에 고정 행을 원하는 개수만큼 만듭니다. 행 구성과 예제는 → [Head / Foot appendix](/docs/appx/head-foot)  
![커스텀 헤드행](/assets/imgs/header3.png "커스텀 헤드행")

---
## 가운데 (데이터)
가운데는 [doSearch()](/docs/funcs/core/do-search), [loadSearchData()](/docs/funcs/core/load-search-data)함수로 조회하거나 [addRow()](/docs/funcs/core/add-row)함수로 추가한 데이터가 보여지는 데이터 영역입니다.  
![데이터 영역](/assets/imgs/body.png "데이터 영역")  
[**데이터 영역**]

---
## 하단 고정

데이터 아래에 고정되어 항상 보이는 부분입니다. 다음 행들이 포함됩니다.

- **합계행(`FormulaRow`)** — 열 합계 등을 자동 계산해 보여주는 행입니다.
- **커스텀 행(`Foot`)** — 데이터 아래에 고정으로 넣는 행입니다.

### *합계 행*
열의 (`col`) [FormulaRow](/docs/props/col/formula-row) 속성을 설정하면 **데이터 아래**에 고정된 합계행이 생겨 합계나 평균 등을 자동 계산해 보여줍니다. (`FormulaRow: "Sum"`, `"Avg"` 등)

![합계행](/assets/imgs/formulaRow.png "합계행")

### *커스텀 행(`Foot`)*
`options.Foot`에 정의해 **데이터 아래**에 고정 행을 만듭니다. 행 구성과 예제는 → [Head / Foot appendix](/docs/appx/head-foot)

![커스텀 풋행](/assets/imgs/foot.png "커스텀 풋행")

---

## 기타

### *솔리드 행*
상단 고정이나 하단 고정 주변에 임의의 행을 추가할 수 있습니다.  
이렇게 추가된 행은 시트 내 열과 무관하게 기능과 크기를 가질 수 있습니다.  
보다 자세한 내용은 (appendix) [Soild](/docs/appx/solid)을 참고하세요.




### *행의 id*
행은 종류(Kind)에 따라 고유 `id`가 자동 부여됩니다. (`AR#` 데이터, `Header`/`HR#` 헤더, `FR#` 하단 고정 등)  
자세한 규칙은 → [Kind appendix](/docs/appx/kind), id로 행을 얻어 값이나 속성을 다루는 법은 → [행 객체 appendix](/docs/appx/row-object)


### Read More
- [ShowFilter cfg](/docs/props/cfg/show-filter)
- [FormulaRow col](/docs/props/col/formula-row)
- [addRow method](/docs/funcs/core/add-row)
- [doSearch method](/docs/funcs/core/do-search)
- [loadSearchData method](/docs/funcs/core/load-search-data)
- [showFilterRow method](/docs/funcs/core/show-filter-row)
- [행 객체 appendix](/docs/appx/row-object)
- [Soild appendix](/docs/appx/solid)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
