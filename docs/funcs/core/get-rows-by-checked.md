# getRowsByChecked ***(method)***

<!-- synonyms: 체크된 행 가져오기, 체크된 row, checked rows, 체크 선택 행, bool true 행 -->

> `Bool` 타입 열에서 체크된 모든 [데이터 로우 객체](/docs/appx/row-object)를 배열로 반환합니다.

### Syntax
```javascript
object getRowsByChecked( col );
```

### Parameters
|Name|Type|Required| Description |
|----------|-----|---|----|
|col | `string` | <span class='required'>필수</span> | 열이름 (`Bool` 타입이어야 함)|

### Return Value
- **배열** — 체크된 행이 있으면 [데이터 로우 객체](/docs/appx/row-object) 배열 (없으면 빈 배열)
- **`false`** — 인자 열이 `Bool` 타입이 아닐 때

### Example
```javascript
// sCheck 열이 체크된 행을 가져와서 처리
var rows = sheet.getRowsByChecked("sCheck");
if (rows && rows.length > 0) {
    for (var i = 0; i < rows.length; i++) {
        console.log(sheet.getValue(rows[i], "sName"));
    }
} else {
    alert("체크된 행이 없습니다.");
}
```

### Read More
- [setCheck method](./set-check)
- [setAllCheck method](./set-all-check)
- [HeaderCheck cfg](/docs/props/cfg/header-check)
- [HeaderCheck col](/docs/props/col/header-check)
- [getDataRows method](./get-data-rows)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.0.0.3|name 인자명 변경 → col, 다른 API와 통일|
