# updatePageLength ***(method)***

> [SearchMode](/docs/props/cfg/search-mode): 5 일 때 한 페이지에 표시할 행의 수를 동적으로 변경할 수 있습니다.

### Syntax
```javascript
boolean updatePageLength( length, cPage );
```

### Parameters
|Name|Type|Required|Description|
|----------|-----|---|----|
|length|`number`|<span class='required'>필수</span>|한 페이지에 표시할 행의 수|
|cPage|`number`|<span class='optional'>선택</span>|한 페이지에 표시할 행의 수 변경 후 이동할 페이지 번호 (`default: 1`)|


### Return Value
***boolean*** : 성공 시 `true`, 실패 시 `false`

### Example
```javascript
// 한 페이지에 보여질 행의 수를 20개로 업데이트 합니다.
sheet.updatePageLength(20);

// 한 페이지에 보여질 행의 수를 30개로 업데이트 하고, 3페이지로 이동합니다.
sheet.updatePageLength(30, 3);
```

### Read More
- [SearchMode cfg](/docs/props/cfg/search-mode)
- [PageLength cfg](/docs/props/cfg/page-length)
- [updateClientPaging method](./update-client-paging)

### Since

|product|version|desc|
|---|---|---|
|core|8.1.0.54|기능 추가|
