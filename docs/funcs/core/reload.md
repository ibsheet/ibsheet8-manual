# reload ***(method)***

<!-- synonyms: 시트 초기화, 시트 재생성, reload sheet, 전체 리셋 -->

> [IBSheet.create({id, el, options, data})](/docs/static/create) 시점의 상태로 시트 전체를 되돌리고, 직전에 데이터를 받은 동작을 다시 실행합니다.  
> 데이터의 값과 상태(Added, Changed, Deleted), 행/셀/컬럼에 부여된 모든 속성이 초기화됩니다.  
> `onRenderFirstFinish`는 다시 발생하지 않으므로, 후처리가 필요하면 `callback`을 사용하세요.

> **데이터 로드 방식별 동작**  
> 
> | 직전에 데이터를 받은 동작 | reload 동작 |
> |---|---|
> | [IBSheet.create({data})](/docs/static/create) | 메모리의 `data`로 다시 로드 |
> | [doSearch](./do-search) | 서버 재조회 |
> | [doSearchPaging](./do-search-paging) | 서버 재조회 (1페이지) |
> | [loadSearchData](./load-search-data) | **빈 시트로 초기화** (재로드 불가) |


### Syntax
```javascript
void reload( callback );
```

### Parameters
|Name|Type|Required| Description |
|----------|-----|---|----|
|callback|`function`|<span class='optional'>선택</span>|`reload` 후, 호출할 콜백 함수 (`onRenderFirstFinish` 와 동일 시점)|


### Return Value
***object*** : 시트 객체

### Example
```javascript
// 시트를 create 시점으로 되돌림
sheet.reload();

// 되돌린 후 데이터 로드
sheet.reload(function (evtParam) {
    evtParam.sheet.loadSearchData(data);
});
```

### Read More

- [reloadData method](./reload-data)
- [dispose method](./dispose)
- [create static](/docs/static/create)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.0.0.26|`callback` 기능 추가|