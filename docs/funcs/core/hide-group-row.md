# hideGroupRow ***(method)***

<!-- synonyms: hideGroupRow, hide-group-row, 그룹 행 숨김, 그룹 행 감춤, 그룹 행 제거, 그룹행 삭제, 그룹 숨기기, hide, group, row, remove -->

> 그룹행을 제거하거나 숨깁니다.

### Syntax
```javascript
void hideGroupRow( del );
```

### Parameters


|Name|Type|Required| Description |
|----------|-----|---|----|
|del |`string or object`|<span class='optional'>선택</span>|그룹행을 삭제합니다. (`default: 1`)|

### Return Value
***boolean*** : 설정 완료 여부

### Example
```javascript
// 그룹행을 제거합니다.
sheet.hideGroupRow(); 

// 그룹행을 숨깁니다.
sheet.hideGroupRow(0); 
```

### Read More

### Since

|product|version|desc|
|---|---|---|
|core|8.3.0.9|기능 추가|
