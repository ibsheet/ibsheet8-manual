# updateClientPaging ***(method)***

> [SearchMode](/docs/props/cfg/search-mode): 1 일 때 한 페이지에 표시할 행의 수를 동적으로 변경할 수 있습니다.

### Syntax
```javascript
boolean updateClientPaging( length, render );
```

### Parameters
|Name|Type|Required|Description|
|----------|-----|---|----|
|length|`number`|<span class='required'>필수</span>|한 페이지에 표시할 행의 수|
|render|`boolean`|<span class='optional'>선택</span>|즉시 화면 반영 여부<br/>해당 기능을 `0(false)`로 사용했을 경우, 작업 마무리 시에 `rerender()`를 실행해야 화면에 반영 됩니다.<br/>`0(false)`:반영 안함<br/>`1(true)`:즉시 반영 (`default`)|


### Return Value
***boolean*** : 성공 시 `true`, 실패 시 `false`

### Example
```javascript
// 한 화면에 보여질 행의 수를 30개로 업데이트 합니다.
sheet.updateClientPaging(30);
```

### Read More
- [SearchMode cfg](/docs/props/cfg/search-mode)
- [PageLength cfg](/docs/props/cfg/page-length)
- [updatePageLength method](./update-page-length)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
