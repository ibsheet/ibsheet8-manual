# AutoFitColWidth ***(cfg)***

<!-- synonyms: AutoFitColWidth, auto fit column width, auto fit col width, fit column width, column width auto, resize column, 자동 컬럼 너비, 자동 열 너비, 컬럼 너비 자동 조정, 열 너비 자동 맞춤, 자동 너비, FitColWidth 자동 호출, 컬럼 크기 자동 -->

> 지정한 시점마다 컬럼 너비 자동 조정 함수 `fitColWidth()`를 호출하여, 각 컬럼의 너비를 시트 전체 너비에 맞게 다시 배분합니다.  
> 컬럼이 넘쳐 가로 스크롤이 생기지 않도록 줄이거나, 오른쪽에 빈 공간이 남지 않도록 늘려 시트 폭에 꽉 차게 맞춥니다.  
> 시트 리사이즈, 조회 등 여러 시점에 컬럼 너비를 자동으로 맞추고 싶을 때 사용하며, 적용할 시점을 구분자 `|` 로 연결하여 설정합니다.  
> **<mark>주의</mark> : [RelWidth](/docs/props/col/rel-width)와 함께 사용할 수 없습니다. RelWidth가 설정된 컬럼이 있으면 이 기능이 정상적으로 동작하지 않습니다.**


### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`search`|데이터를 조회하거나 로드할 때 (`doSearch` / `loadSearchData`)|
|`resize`|시트 크기가 조정될 때|
|`init`|시트를 처음 생성할 때 (`create`)|
|`colhidden`|컬럼을 숨기거나 다시 보일 때|
|`rowtransaction`|행을 추가/삭제하거나 숨김/보임 한 뒤|
|`colresize`|컬럼 너비를 변경한 뒤 (변경한 컬럼은 제외하고 나머지 컬럼만 재조정)|

> `rowtransaction`은 행이 늘거나 줄면서 세로 스크롤바가 생기거나 사라질 때, 그만큼 표시 폭이 달라져 가로 스크롤이 생기는 것을 막기 위한 시점입니다.

### Example
```javascript
// 시트 생성 시점과 데이터 조회/로드 시점에 컬럼 너비를 자동으로 조정
options = {
  Cfg: {
    AutoFitColWidth: 'init|search'
  }
};
```

### Read More
- [fitColWidth method](/docs/funcs/core/fit-col-width)


### Since

|product|version|desc|
|---|---|---|
|core|8.4.0.6|기능 추가|
