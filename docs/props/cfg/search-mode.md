# SearchMode ***(cfg)***

<!-- synonyms: 조회모드, 페이징, 서버페이징, 스크롤, 클라이언트 페이징, search mode, paging, server paging, lazy load, fast load, scroll append -->

> 데이터를 조회하고 화면에 표시하는 방식을 설정합니다.  
> - 데이터를 한번에 전체 조회할 수 있으면 → `0`, `1`, `2`를 설정합니다.  
> - 데이터가 많아 서버·브라우저 메모리 부족이나 렌더링 부담이 크면 → `3`, `4`, `5`를 설정합니다.  

### Type
`number`

### Options
|Value|Mode|Description|
|-----|-----|------|
|`0`|**FastLoad**|전체 데이터를 조회하고 세로 스크롤 시 보이는 셀의 데이터만 교체하여 표시|
|`1`|**ClientPaging**|전체 데이터를 조회하고 [PageLength](./page-length) 만큼 페이징 처리|
|`2`|**LazyLoad (default)**|전체 데이터를 조회하고 스크롤 위치에 따라 [PageLength](./page-length) 단위로 표시|
|`3`|**ScrollAppend**|데이터가 많아 서버 응답이 느리거나 브라우저 렌더링 부담이 큰 경우 사용.<br/>[PageLength](./page-length) 단위로 서버에서 조회<br/>스크롤 하단 도달 시 추가 조회하여 기존 데이터 하단에 표시.<br/>조회한 페이지는 재요청 없음|
|`4`|**ServerPaging**|데이터가 많아 서버 응답이 느리거나 브라우저 렌더링 부담이 큰 경우 사용.<br/>[PageLength](./page-length) 단위로 서버에서 조회<br/>페이지 번호 클릭 시 해당 페이지 데이터를 조회하여 표시.<br/>조회한 페이지는 재요청 없음|
|`5`|**ServerPaging2**|데이터가 많아 서버 응답이 느리거나 브라우저 렌더링 부담이 큰 경우 사용.<br/>ServerPaging과 동일하나 페이지 이동 시 항상 서버 재요청|

### 비교표

|구분|0<br/>(FastLoad)|1<br/>(ClientPaging)|2<br/>(LazyLoad)|3<br/>(ScrollAppend)|4<br/>(ServerPaging)|5<br/>(ServerPaging2)|
|---|---|---|---|---|---|---|
|데이터<br/>로드|전체 데이터 조회|전체 데이터 조회|전체 데이터 조회|서버에서 PageLength 단위 조회|서버에서 PageLength 단위 조회|서버에서 PageLength 단위 조회|
|조회<br/>함수|doSearch<br/>loadSearchData|doSearch<br/>loadSearchData|doSearch<br/>loadSearchData|doSearchPaging|doSearchPaging|doSearchPaging|
|페이지<br/>번호|X|O<br/>(InfoRowConfig)|X|X|O<br/>(InfoRowConfig)|O<br/>(InfoRowConfig)|
|페이지<br/>캐싱|—|—|—|O<br/>(재요청 없음)|O<br/>(재요청 없음)|X<br/>(항상 재요청)|
|서버 응답에<br/>Total 필수|X|X|X|O|O|O|
|Sort|전체 데이터|전체 데이터|전체 데이터|조회된 데이터에서만 정렬<br/>(서버로 Sort 정보 전송 시 ScrollPagingServerSort 참조)|서버로 Sort 정보 전송<br/>(조회된 데이터에서만 정렬 시 SortCurrentPage 참조)|서버로 Sort 정보 전송<br/>(조회된 데이터에서만 정렬 시 SortCurrentPage 참조)|
|Filter|전체 데이터|전체 데이터|전체 데이터|조회된 데이터만<br/>(전체는 서버 재조회: onBeforeFilter)|조회된 데이터만<br/>(전체는 서버 재조회: onBeforeFilter)|조회된 데이터만<br/>(전체는 서버 재조회: onBeforeFilter)|
|찾기<br/>(Ctrl+F)|전체 데이터|전체 데이터|전체 데이터|조회된 데이터만|조회된 데이터만|조회된 데이터만|
|Pivot|O|O|O|X|X|X|
|엑셀<br/>다운로드|전체 데이터|전체 데이터|전체 데이터|조회된 데이터만<br/>(서버에서 전체 다운로드: directDown2Excel)|조회된 데이터만<br/>(서버에서 전체 다운로드: directDown2Excel)|PageLength 만큼<br/>(서버에서 전체 다운로드: directDown2Excel)|
|Tree|O|X|O|X|X|X|
|FormulaRow|O|O|O|△<br/>(대안: Foot 또는 showFixedRows)|△<br/>(대안: Foot 또는 showFixedRows)|△<br/>(대안: Foot 또는 showFixedRows)|
|makeSubTotal|O|X|O|X|X|X|
|Wrap, Lines,<br/>Image 등<br/>가변 행 높이|AutoRowHeight<br/>필요|O|O|AutoRowHeight<br/>필요|O|O|

### 모드 선택 가이드

먼저 **데이터를 한 번에 전체 조회할 수 있는지**로 크게 나눕니다.

- **전체 데이터를 한 번에 받아도 무리 없으면 → `0` / `1` / `2`** (조회: [doSearch](/docs/funcs/core/do-search) / [loadSearchData](/docs/funcs/core/load-search-data))
  - `0` **FastLoad** — 세로 스크롤이 부드럽고 렌더링 성능에 가장 유리. 단, 행 높이가 모두 같아야 하며 가변이면 [AutoRowHeight](./auto-row-height)가 필요합니다.
  - `1` **ClientPaging** — **페이지 번호로 나눠** 보여줄 때. (`Tree`, `makeSubTotal` 미지원)
  - `2` **LazyLoad (기본)** — 일반적인 경우. `Tree`, `makeSubTotal`, 가변 행 높이까지 폭넓게 지원합니다.
- **데이터가 많아 한 번에 받기 부담되면**(서버 응답 지연, 메모리, 렌더링 부담) **→ `3` / `4` / `5`** (조회: [doSearchPaging](/docs/funcs/core/do-search-paging), 서버 응답에 `Total` 필요)
  - `3` **ScrollAppend** — 스크롤을 내리면 다음 페이지를 **이어 붙이는** 방식.
  - `4` **ServerPaging** — **페이지 번호**로 이동(조회한 페이지는 캐싱).
  - `5` **ServerPaging2** — 페이지 이동 시 **항상 서버를 재조회**(최신 데이터 반영이 중요할 때).

> 정확한 데이터 건수 기준선은 컬럼 수, 셀 내용, 서버 환경에 따라 달라지므로 단정하기 어렵습니다.  
> 전체를 한 번에 받았을 때 부담이 없으면 `0`~`2`, 그렇지 않으면 `3`~`5`를 기준으로 삼고, 필요한 기능은 위 **비교표**에서 확인하세요.  
> 예를 들어 `Pivot`, `Tree`, `makeSubTotal`, `(Col) FormulaRow`는 서버 페이징(`3`/`4`/`5`)에서 제약이 있습니다.

### SearchMode: 0 (FastLoad)

가상 스크롤 기반으로, 사용자가 세로 스크롤 시 보이는 영역의 데이터만 즉시 갱신합니다.  
스크롤과 동시에 화면의 끊김 없이 행의 데이터를 바로 확인할 수 있습니다.

> 각 행의 높이는 모두 동일해야 하며, [(Appendix)기능에 제약사항](/docs/appx/fastload-constraints)이 있습니다.  
> 데이터행의 높이가 일정하지 않다면 [(Cfg)AutoRowHeight](./auto-row-height)를 설정하시기 바랍니다.

> FastLoad는 화면에 보이는 셀(보이는 행 × 열)만큼 렌더하므로, 시트 높이가 크거나 컬럼이 많으면 한 번에 그리는 셀이 많아져 렌더 부담이 커질 수 있습니다.  
> 컬럼이 많은 경우 [(Cfg)ColPage](./col-page)(보이는 컬럼만 렌더), [(Cfg)NoRenderHidden](./no-render-hidden)(숨긴 컬럼 미렌더)으로 완화할 수 있습니다.

```javascript
options.Cfg = { SearchMode: 0 };

// AJAX 통신으로 조회
sheet.doSearch({ url: "/api/data.jsp", method: "POST" });

// 또는 데이터 직접 바인딩
sheet.loadSearchData({ data: jsonData });
```

### SearchMode: 1 (ClientPaging)

전체 데이터를 조회하고 [(Cfg)PageLength](./page-length) 설정값만큼 페이징 처리 후 페이지 번호를 통해 보여주는 기능입니다.

- [(Method)updateClientPaging](/docs/funcs/core/update-client-paging) 함수를 이용해서 동적으로 페이지의 개수를 변경하고 재계산할 수 있습니다.
- [InfoRowConfig](./info-row-config)를 사용해 페이지 번호를 표시해야 페이지를 클릭하여 이동할 수 있습니다.

> **주의** : `(Method) makeSubTotal` 지원하지 않습니다.

```javascript
// 기본 페이지 번호
options.Cfg = {
    SearchMode: 1,
    PageLength: 50,
    InfoRowConfig: { Layout: ["Paging", "Count"] }
};

// 숫자형 페이지 번호 + 페이지 크기 선택
options.Cfg = {
    SearchMode: 1,
    PageLength: 50,
    InfoRowConfig: {
        Layout: ["Paging2", "Count"],
        ViewCount: 1,
        ViewFormat: "10|20|50|100"
    }
};

// AJAX 통신으로 조회
sheet.doSearch({ url: "/api/data.jsp", method: "POST" });

// 또는 데이터 직접 바인딩
sheet.loadSearchData({ data: jsonData });
```

### SearchMode: 2 (LazyLoad) — default

가상 스크롤 기반으로, 전체 데이터를 조회하고 [(Cfg)PageLength](./page-length) 설정값 단위로 스크롤 위치에 따라 데이터를 화면에 표시하는 기능입니다.

```javascript
options.Cfg = { SearchMode: 2, PageLength: 50 };

// AJAX 통신으로 조회
sheet.doSearch({ url: "/api/data.jsp", method: "POST" });

// 또는 데이터 직접 바인딩
sheet.loadSearchData({ data: jsonData });
```

### SearchMode: 3 (ScrollAppend)

[(Cfg)PageLength](./page-length)에 지정된 개수만큼 한 페이지씩 서버에서 조회하여 화면에 표시하는 기능입니다.

- 조회는 반드시 [(Method)doSearchPaging](/docs/funcs/core/do-search-paging) 함수를 통해 수행해야 합니다.
- 세로 스크롤이 하단에 도달하면 다음 페이지 데이터를 서버에서 조회하여 기존 데이터 아래에 추가합니다.
- 서버는 시트로부터 넘어오는 페이지 정보(`ibpage=2,3,4...`)에 따라 페이징 쿼리를 구성하여 각 페이지별 데이터를 리턴해야 합니다.
- 조회 데이터에 **Total**(전체 record 수) 속성이 포함되어 있어야 합니다.
- **Total** 값과 누적 데이터 수가 같아지면 더 이상 서버 호출은 발생하지 않습니다.
- 한번 조회한 페이지는 재요청 없이 재사용됩니다.
- `Sort`, `Filter`, `엑셀 다운로드`는 기본적으로 조회된 데이터 안에서만 동작합니다.
  - `Sort` : [(Cfg) ScrollPagingServerSort](./scroll-paging-server-sort)를 설정하면 서버로 정렬 요청을 전송할 수 있습니다.
  - `엑셀 다운로드` : [(Method) directDown2Excel](/docs/funcs/excel/direct-down-to-excel)을 사용하면 전체 데이터를 다운로드할 수 있습니다.
    단, 서버에서 전체 데이터를 처리할 수 있는 메모리가 충분해야 합니다.
  - `Filter` : 전체 데이터에 대한 필터링은 지원하지 않습니다. 단, [onBeforeFilter](/docs/events/on-before-filter)에서 [getFilter](/docs/funcs/core/get-filter)로 필터 조건을 모아 [doSearchPaging](/docs/funcs/core/do-search-paging)로 서버에 전송하면(기본 필터는 `return 1`로 취소) 전체 데이터 기준 필터를 서버에서 구현할 수 있습니다.
- `(Col) FormulaRow`는 사용할 수 없습니다. 전체 합계가 필요한 경우 서버에서 계산하여 [Foot](/docs/start/row) 또는 [showFixedRows](/docs/funcs/core/show-fixed-rows)로 Footer에 표시합니다.
- `(Method) makeSubTotal`은 지원하지 않습니다.

> **주의**
> - `Type:Lines, Img`나 `Wrap:1` 과 같이 데이터 행의 높이가 일정하지 않은 속성을 사용하려면 [(Cfg)AutoRowHeight](./auto-row-height)를 설정해야 합니다.

```javascript
options.Cfg = { SearchMode: 3, PageLength: 50 };

// doSearchPaging으로 최초 조회
// 이후 페이지 이동, Sort 등은 시트가 자동으로 서버에 요청합니다.
sheet.doSearchPaging({ url: "/api/data.jsp", method: "POST" });
```

### SearchMode: 4 (ServerPaging)

[(Cfg)PageLength](./page-length)에 지정된 개수만큼 한 페이지씩 서버에서 조회하여 화면에 표시하는 기능입니다.

- 조회는 반드시 [(Method)doSearchPaging](/docs/funcs/core/do-search-paging) 함수를 통해 수행해야 합니다.
- [InfoRowConfig](./info-row-config)를 사용해 페이지 번호를 표시해야 페이지를 클릭하여 이동할 수 있습니다.
- 페이지 번호 변경 시 doSearchPaging이 호출한 URL을 다시 요청하여 해당 페이지 데이터를 표시합니다.
- 서버는 시트로부터 넘어오는 페이지 정보(`ibpage=2,3,4...`)에 따라 페이징 쿼리를 구성하여 각 페이지별 데이터를 리턴해야 합니다.
- 조회 데이터에 **Total**(전체 record 수) 속성이 포함되어 있어야 합니다.
- 한번 조회한 페이지는 서버를 다시 호출하지 않습니다.
- `Sort`는 기본적으로 서버로 정렬 정보를 전송하므로, 서버에서 정렬된 결과를 조회해야 합니다. 조회된 데이터에서만 정렬하려면 [SortCurrentPage](./sort-current-page)를 설정하세요.
- `Filter`, `엑셀 다운로드`는 조회된 데이터 안에서만 동작합니다.
  - `엑셀 다운로드` : [(Method) directDown2Excel](/docs/funcs/excel/direct-down-to-excel)을 사용하면 전체 데이터를 다운로드할 수 있습니다.
    단, 서버에서 전체 데이터를 처리할 수 있는 메모리가 충분해야 합니다.
  - `Filter` : 전체 데이터에 대한 필터링은 지원하지 않습니다. 단, [onBeforeFilter](/docs/events/on-before-filter)에서 [getFilter](/docs/funcs/core/get-filter)로 필터 조건을 모아 [doSearchPaging](/docs/funcs/core/do-search-paging)로 서버에 전송하면(기본 필터는 `return 1`로 취소) 전체 데이터 기준 필터를 서버에서 구현할 수 있습니다.
- `(Col) FormulaRow`는 사용할 수 없습니다. 전체 합계가 필요한 경우 서버에서 계산하여 [Foot](/docs/start/row) 또는 [showFixedRows](/docs/funcs/core/show-fixed-rows)로 Footer에 표시합니다.
- `(Method) makeSubTotal`은 지원하지 않습니다.

```javascript
// 기본 페이지 번호
options.Cfg = {
    SearchMode: 4,
    PageLength: 50,
    InfoRowConfig: { Layout: ["Paging", "Count"] }
};

// 숫자형 페이지 번호 + 건수 포맷 커스텀
options.Cfg = {
    SearchMode: 4,
    PageLength: 50,
    InfoRowConfig: {
        Layout: ["Paging2", "Count"],
        ViewCount: 1,
        Format: "[BOTTOMDATAROW / TOTALROWS] 건"
    }
};

// doSearchPaging으로 최초 조회
// 이후 페이지 이동, Sort 등은 시트가 자동으로 서버에 요청합니다.
sheet.doSearchPaging({ url: "/api/data.jsp", method: "POST" });
```

### SearchMode: 5 (ServerPaging2)

[(Cfg)PageLength](./page-length)에 지정된 개수만큼 한 페이지씩 서버에서 조회하여 화면에 표시하는 기능입니다.
`ServerPaging`과 동일하지만, 페이지 이동 시 항상 서버를 호출하여 최신 데이터를 조회합니다.

- 조회는 반드시 [(Method)doSearchPaging](/docs/funcs/core/do-search-paging) 함수를 통해 수행해야 합니다.
- [InfoRowConfig](./info-row-config)를 사용해 페이지 번호를 표시해야 페이지를 클릭하여 이동할 수 있습니다.
- 서버는 시트로부터 넘어오는 페이지 정보(`ibpage=2,3,4...`)에 따라 페이징 쿼리를 구성하여 각 페이지별 데이터를 리턴해야 합니다.
- 조회 데이터에 **Total**(전체 record 수) 속성이 포함되어 있어야 합니다.
- 페이지 이동 시 항상 서버를 재요청합니다. (캐싱 없음)
- `Sort`는 기본적으로 서버로 정렬 정보를 전송하므로, 서버에서 정렬된 결과를 조회해야 합니다. 조회된 데이터에서만 정렬하려면 [SortCurrentPage](./sort-current-page)를 설정하세요.
- `Filter`, `엑셀 다운로드`는 조회된 데이터(PageLength) 안에서만 동작합니다.
  - `엑셀 다운로드` : [(Method) directDown2Excel](/docs/funcs/excel/direct-down-to-excel)을 사용하면 전체 데이터를 다운로드할 수 있습니다.
    단, 서버에서 전체 데이터를 처리할 수 있는 메모리가 충분해야 합니다.
  - `Filter` : 전체 데이터에 대한 필터링은 지원하지 않습니다. 단, [onBeforeFilter](/docs/events/on-before-filter)에서 [getFilter](/docs/funcs/core/get-filter)로 필터 조건을 모아 [doSearchPaging](/docs/funcs/core/do-search-paging)로 서버에 전송하면(기본 필터는 `return 1`로 취소) 전체 데이터 기준 필터를 서버에서 구현할 수 있습니다.
- `(Col) FormulaRow`는 사용할 수 없습니다. 전체 합계가 필요한 경우 서버에서 계산하여 [Foot](/docs/start/row) 또는 [showFixedRows](/docs/funcs/core/show-fixed-rows)로 Footer에 표시합니다.
- `(Method) makeSubTotal`은 지원하지 않습니다.
- [(Method)updatePageLength](/docs/funcs/core/update-page-length)를 통해 동적으로 페이지 행의 개수를 변경할 수 있습니다.

```javascript
// 숫자형 페이지 번호 + 페이지 크기 선택
options.Cfg = {
    SearchMode: 5,
    PageLength: 50,
    InfoRowConfig: {
        Layout: ["Paging2", "Count"],
        ViewCount: 1,
        ViewFormat: "10|20|50|100"
    }
};

// doSearchPaging으로 최초 조회 (항상 서버 재요청)
// 이후 페이지 이동, Sort 등은 시트가 자동으로 서버에 요청합니다.
sheet.doSearchPaging({ url: "/api/data.jsp", method: "POST" });
```

### Read More
- [AutoRowHeight cfg](./auto-row-height)
- [InfoRowConfig cfg](./info-row-config)
- [PageLength cfg](./page-length)
- [SortCurrentPage cfg](./sort-current-page)
- [ScrollPagingServerSort cfg](./scroll-paging-server-sort)
- [조회 응답 규격](/docs/dataStructure/data-structure)
- [페이징 응답 규격](/docs/dataStructure/paging-structure)
- [doSearch method](/docs/funcs/core/do-search)
- [loadSearchData method](/docs/funcs/core/load-search-data)
- [doSearchPaging method](/docs/funcs/core/do-search-paging)
- [updateClientPaging method](/docs/funcs/core/update-client-paging)
- [updatePageLength method](/docs/funcs/core/update-page-length)
- [showFixedRows method](/docs/funcs/core/show-fixed-rows)
- [directDown2Excel method](/docs/funcs/excel/direct-down-to-excel)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.1.0.54|`ServerPaging2` 추가|