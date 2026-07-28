# Kind ***(appendix)***
> **행(Row)** 은 시트의 가로줄이고, **Kind** 는 그 행의 **종류(역할)** 입니다.  
> 모든 행은 Kind를 하나 가지며 [getRowKind](/docs/funcs/core/get-row-kind)로 확인합니다.  
> 헤더와 데이터 같은 기본 종류부터, 헤더 아래의 필터나 그룹 등 다양한 종류가 있습니다.  
> Kind(종류)는 행이 **어느 영역(헤더, 바디, 푸터)에 있는지**(위치)와는 **다른 축**입니다. 위치 기준 설명은 [행(Row) 구조](/docs/start/row)를 참고하세요.

### Kind의 종류
|Kind|Description|
|---|---|
|*Group*|헤더 상단에 위치하여 지정한 열에 대한 그룹핑 기능을 수행합니다.<br/>![그룹](/assets/imgs/groupRow.png "그룹행")|
|*Header*|데이터 영역 상단에 항상 보여지게 되는 행으로 열의 위치 변경, 소팅 등의 기본적인 기능을 가지고 있습니다.<br/>![헤더](/assets/imgs/header.png "헤더행")|
|*Filter*|헤더와 데이터 영역 사이에 위치하며, 각 셀에 값을 입력시 열 별로 해당 값을 포함하는 행만 남기고 나머지 행을 감추는 기능을 가지고 있습니다.<br/>![필터](/assets/imgs/filter.png "필터행")|
|*Search*|필터와 데이터 행 사이에 위치하여 입력한 값을 포함하는 행만 남기고 나머지 행을 감추는 기능을 합니다.<br/>![찾기](/assets/imgs/searchRow.png "찾기행")|
|*Data*|일반적인 데이터 행입니다.<br/>![데이터](/assets/imgs/dataRow.png "데이터행")|
|*Head*|헤더 행 아래 고정된 행을 의미합니다.<br/>![Head](/assets/imgs/kindHead.png "Head")|
|*Foot*|합계 행이나 데이터 행 아래 고정된 행을 의미합니다.<br/>![Head](/assets/imgs/kindFoot.png "Head")|
|*Space*|빈 공간의 행으로 시트 내의 열의 너비에 영향을 받지 않는 다양한 셀 객체를 넣을 수 있습니다.(일반적인 솔리드 행)<br/>또한 행의 위치도 헤더의 위나, 푸터의 위나 아래 등 다양한 곳에 위치할 수 있습니다.<br/>![스페이스](/assets/imgs/spaceRow.png "스페이스행")|

> `Group`, `Search`, `Space`(일반 솔리드) 행은 시트가 자동으로 만드는 것이 아니라 **`options.Solid`로 직접 만듭니다.** `Group`과 `Search`는 솔리드의 예약 기능입니다. → [Solid appendix](/docs/appx/solid)

### 행 id
`id`는 각 행을 구별하는 **고유 이름**입니다. [getRowById](/docs/funcs/core/get-row-by-id)로 특정 행을 집어 값이나 속성을 다룰 때 사용하며, 종류에 따라 아래처럼 자동으로 붙습니다.

|종류|자동 `id`|설명|
|---|---|---|
|데이터(`Data`)|`AR1`, `AR2` …|조회하거나 추가한 순서대로 번호가 붙습니다.|
|헤더(`Header`)|`Header`, `HR1`, `HR2` …|첫 헤더행은 `Header`, 두 번째 헤더행부터 `HR1`, `HR2` … 입니다.|
|필터(`Filter`)|`Filter`|필터행은 항상 `Filter` 입니다.|
|합계행(`FormulaRow`)|`FormulaRow`|합계행은 항상 `FormulaRow` 입니다.|
|커스텀 `Head`/`Foot`/Solid|직접 지정한 `id`|만들 때 준 `id`를 씁니다. 지정하지 않으면 `Head`는 **헤더행과 `HR#`를 공유**(헤더행 다음 번호), `Foot`은 `FR1`, `FR2` … 로 붙습니다. → [Head / Foot appendix](/docs/appx/head-foot)|

자동 번호(`AR#`, `HR#`, `FR#`)는 행이 추가되거나 삭제되면 밀릴 수 있으니, 특정 행을 안정적으로 참조하려면 커스텀 행에는 `id`를 직접 지정하세요. 얻은 행으로 값이나 속성을 다루는 법은 → [행 객체 appendix](/docs/appx/row-object)

### Read More
- [Kind row](/docs/props/row/kind)
- [getRowKind method](/docs/funcs/core/get-row-kind)
- [Solid appendix](/docs/appx/solid)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
