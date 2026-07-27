# reloadData ***(method)***

<!-- synonyms: 데이터 다시 로드, 데이터 재조회, reload data, 시트 재로드 -->

> 시트의 현재 데이터를 비우고, 직전에 데이터를 받은 동작을 다시 실행합니다.  
> 데이터의 값과 상태(Added, Changed, Deleted), 행과 셀에 부여된 속성은 초기화되며, 컬럼에 부여된 속성은 그대로 유지됩니다.  
> `Head`, `Foot`, `Solid` 영역에는 영향을 주지 않습니다.

> **데이터 로드 방식별 동작**  
> 
> | 직전에 데이터를 받은 동작 | reloadData 동작 |
> |---|---|
> | [IBSheet.create({data})](/docs/static/create) | 메모리의 `data`로 다시 로드 |
> | [doSearch](./do-search) | 서버 재조회 |
> | [doSearchPaging](./do-search-paging) | 서버 재조회 (1페이지) |
> | [loadSearchData](./load-search-data) | **빈 시트로 초기화** (재로드 불가) |

> **reloadData vs revertData**  
> `reloadData`는 현재 행을 모두 비우고 다시 로드합니다 — 행 자체를 재생성합니다.  
> [revertData](./revert-data)는 각 셀의 [Orig](/docs/props/cell/orig)(최초 로딩 값)으로 셀 값만 복원합니다 — 시트의 행은 그대로 유지됩니다.

### Syntax
```javascript
void reloadData( func );
```

### Parameters
|Name|Type|Required| Description |
|----------|-----|---|----|
|func |`function`|<span class='optional'>선택</span>|리로드 완료 후 콜백 정의|

### Return Value
***none***

### Example
```javascript
// create 시점의 데이터로 되돌림
sheet.reloadData();

// 완료 후 콜백 실행
sheet.reloadData(function() {
    console.log("데이터가 초기화되었습니다.");
});
```

### Read More

- [reload method](./reload)
- [revertData method](./revert-data)
- [create static](/docs/static/create)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
