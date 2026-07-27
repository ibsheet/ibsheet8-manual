# revertData ***(method)***

<!-- synonyms: 시트 되돌리기, 데이터 복원, revert data, 전체 변경 취소 -->

> 시트 전체 데이터를 조회된 데이터로 되돌립니다.  
> 데이터의 값과 상태(Added, Changed, Deleted)만 되돌리며, 행/셀/컬럼에 부여된 속성은 그대로 유지됩니다.

### Syntax
```javascript
void revertData( remainAddRow, sync );
```

### Parameters
|Name|Type|Required| Description |
|----------|-----|---|----|
|remainAddRow|`boolean`|<span class='optional'>선택</span>|[addRow](./add-row)로 추가된 행을 남길지에 대한 여부<br>`0(false)`:추가된 행 모두 삭제 (`default`)<br/>`1(true)`:추가된 행 유지|
|sync|`boolean`|<span class='optional'>선택</span>|렌더링 작업을 동기로 처리 <br/>`0(false)`:비동기 방식 (`default`)<br/>`1(true)`:동기 방식|

### Return Value
***none***

### Example
```javascript
// 시트 전체 데이터 되돌림 (추가된 행 모두 삭제 + 비동기 렌더링, 모두 default)
sheet.revertData();

// 추가된 행은 유지하면서 데이터 되돌림
sheet.revertData(true);

// 동기 렌더링으로 되돌림 (추가된 행은 삭제)
sheet.revertData(false, true);
```

### Read More

- [revertRow method](./revert-row)
- [revertCell method](./revert-cell)
- [reloadData method](./reload-data)
- [Orig cell](/docs/props/cell/orig)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.7|기능 추가|
|core|8.0.0.26|`sync` 인자 추가|
