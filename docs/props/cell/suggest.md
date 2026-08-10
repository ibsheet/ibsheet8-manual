# Suggest ***(cell)***

<!-- synonyms: 서제스트, 자동완성, 자동 완성, 추천어, 추천 목록, 검색 자동완성, 입력 자동완성, 자동 추천, 셀 자동완성, suggest, autocomplete, autosuggest, typeahead, suggestion list -->

> 포탈 사이트 검색창의 자동완성과 마찬가지로 셀 안에 들어갈 내용 리스트를 정의해 두면, 입력시 리스트 중에 시작글자가 동일한 값이 필터링되어 보여집니다. 
>
> 첫번째 글자를 구분자로 하는 문자열로 설정합니다.

###
![Suggest](/assets/imgs/suggest.gif "Suggest")


### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`string`|첫글자를 구분자로 하는 문자열 ( ex: "\|우럭\|광어\|참돔\|볼락\|도다리\|부시리")


### Example
```javascript
//1. 메소드를 통해 특정 셀에 속성 적용 (열이름: CLS)
sheet.setAttribute(sheet.getRowById("AR99"), "CLS", "Suggest", "|싼타페 현대|포터2 현대|그랜저 현대|카니발 기아...");


//2. 객체에 직접 접근해서 속성 적용 (열이름: CLS)
var ROW = sheet.getRowById("AR10");
ROW["CLSSuggest"] = "|항공|철도|도로";
//변경내용 확인
sheet.refreshCell({row:ROW, col:"CLS"});


//3. 조회 데이터 내에서 속성 적용 (열이름: CLS)
{
    data:[
        {... , "CLSSuggest":"|노인우대|장애인|아동|유아" , ...}
    ]
}
```

### Read More
- [SuggestType cell](./suggest-type)
- [SuggestMin cell](./suggest-min)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
