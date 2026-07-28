# tree(트리) 응답 규격 ***(tree response structure)***
doSearch 또는 loadSearchData 함수로 바인딩되는 `tree(트리) 데이터 구조`를 정의합니다.


## Tree(트리) 응답 규격

### 일반적인 tree(트리) 데이터 형태
- 서버 응답 데이터는 `Data` 속성을 최상위로 가지고 있으며, `Data` 속성 안에는 각각의 항목이 객체 형태로 들어 있는 배열이 포함되어 있습니다.
- 하위 행이 존재하는 경우, 해당 객체의 `Items` 속성에 자식 행이 배열 형태로 포함되며, 이를 통해 `트리(Tree) 구조`의 데이터를 표현합니다. 
```js
// Items 속성안에 자식 행을 추가하는 형태로 구성
{"Data":
    [
        //1 Depth
        {sProduct:"내부 시스템 개발 사업",sCustomer:"B사",sDate:"20180116", sCustomerRowSpan:2,
            //2 Depth
            Items:[
                {sProduct:"글로벌 통합 인사시스템",sKind:"프로젝트", sCount:"1",sPrice:"192"},
                {sProduct:"LEGACY SW 공급",sKind:"소프트웨어", sCount:"1",sPrice:"420"}
            ]
        },
        //1 Depth
        {sProduct:"복무급여고도화시스템",sCustomer:"D사",sDate:"20171031",
            //2 Depth
            Items:[
                {sProduct:"병원 전자구매 및 조달시스템",sKind:"납품",sCount:"1",sPrice:"303",sDiscount:"10" }
            ]
        },
        //1 Depth
        {sProduct:"2017~2018 솔루션 납품 및 판매",sCustomer:"E사",sDate:"20170520",
            //2 Depth
            Items:[
                {sProduct:"병원 개발/CDP 구축",sKind:"프로젝트",sCount:"1",sPrice:"29"},
                {sProduct:"성능개량사업 군수지원교보재",sKind:"프로젝트",sCount:"1",sPrice:"15.5",sDiscount:"5"},
                {sProduct:"SHE시스템 구축",sKind:"프로젝트",sCount:"1",sPrice:"79"},
                {sProduct:"Cost Quotation System",sKind:"프로젝트",sCount:"1",sPrice:"3"},
                {sProduct:"전사업무지원시스템",sKind:"프로젝트",sCount:"1",sPrice:"59.5"},
                {sProduct:"통합판매관리시스템",sKind:"프로젝트",sCount:"1",sPrice:"39"},
                {sProduct:"E-HR시스템",sKind:"유지보수",
                    //3 Depth
                    Items:[
                        {sProduct:"물산 E-HR시스템",sKind:"기타",sCount:"1",sPrice:"4"},
                        {sProduct:"제조 E-HR시스템",sKind:"기타",sCount:"1",sPrice:"4" }
                    ]
                },
                {sProduct:"건설 외주실적 단가시스템",sKind:"납품",sCount:"1",sPrice:"95"},
                {sProduct:"인재육성시스템",sKind:"프로젝트",sCount:"1",sPrice:"7"},
                {sProduct:"웹사이트 액티브X제거 관련 SW 구매",sKind:"프로젝트", sCount:"1",sPrice:"22.5" }
        ]}
    ]
}
```

### 간단한 tree(트리) 데이터 형태
- Items 기반의 데이터 구조를 사용할 수 없는 경우, 각 데이터 객체에 `Level` 값을 지정하여 계층 구조를 표현할 수 있습니다.
- 최상위 노드는 `0`부터 시작해야 하며, 하위 노드는 `부모 노드보다 1씩 증가한 값`으로 순차적으로 설정해야 합니다.
```js
var treeData = {
    "Data":[
        {Level:0 ,sProduct:"병원 개발/CDP 구축",sKind:"프로젝트",sCount:"1",sPrice:"29"},
        {Level:1 ,sProduct:"성능개량사업 군수지원교보재",sKind:"프로젝트",sCount:"2",sPrice:"15.5",sDiscount:"5"},
        {Level:2 ,sProduct:"SHE시스템 구축",sKind:"프로젝트",sCount:"1",sPrice:"79"},
        {Level:2 ,sProduct:"Cost Quotation System",sKind:"프로젝트",sCount:"1",sPrice:"3"},
        {Level:3 ,sProduct:"전사업무지원시스템",sKind:"프로젝트",sCount:"1",sPrice:"59.5"},
        {Level:3 ,sProduct:"통합판매관리시스템",sKind:"프로젝트",sCount:"1",sPrice:"39"},
    ]
}
```
- 위와 같이 `Level` 값을 포함한 데이터는 `ibsheet-common.js`파일에서 제공하는 `convertTreeData`함수를 통해 Items 기반의 tree(트리) 구조로 변환됩니다. (Level의 대소문자 주의)
```js
var convertData = IBSheet.v7.convertTreeData(treeData);
sheet.loadSearchData(convertData);
```
- `doSearch` 함수로 조회하는 경우 `onReceiveData`이벤트에서 처리 가능 합니다.


### 동적 트리 조회 (자식 행 동적 로드)
- 트리 데이터가 많아 한 번에 조회하기 어려운 경우, 상위 레벨만 먼저 받고 사용자가 행을 펼치는 시점에 자식을 동적으로 조회해 추가하는 형태로 구성할 수 있습니다.
- 자식이 있을 것으로 예상되는 행에 `HaveChild:true`를 표기하면 트리 아이콘이 표시됩니다. 펼치는 시점에 `onBeforeExpand` 이벤트에서 자식을 조회해 `loadSearchData` 또는 `doSearch`의 `parent` 인자로 부모 행 아래에 추가합니다.
```js
// 초기 0~1레벨 응답 — 1레벨 중 자식이 있는 행은 HaveChild:true로 표시
{"Data":
    [
        {Dept:"본부장", Items:[
            {Dept:"팀장A", HaveChild:true},
            {Dept:"팀장B"}
        ]},
        {Dept:"임원A", Items:[
            {Dept:"팀장X", HaveChild:true}
        ]},
        {Dept:"사원X"}
    ]
}
```
```js
// 펼침 시점 자식 응답 — 부모(팀장A) 아래에 추가될 자식 데이터
{"Data":
    [
        {Dept:"사원1"},
        {Dept:"사원2"}
    ]
}
```
- 자세한 코드 패턴(이벤트 핸들러, 캐시 등)은 [HaveChild (row)](/docs/props/row/have-child)를 참고하세요.


### Read More
- [MainCol cfg](/docs/props/cfg/main-col)
- [doSearch method](/docs/funcs/core/do-search)
- [loadSearchData method](/docs/funcs/core/load-search-data)
- [getChangedData method](/docs/funcs/core/get-changed-data)
- [onReceiveData](/docs/events/on-receive-data)
- [onBeforeDataLoad](/docs/events/on-before-data-load)
- [onDataLoad](/docs/events/on-data-load)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
