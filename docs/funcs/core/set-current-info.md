# setCurrentInfo ***(method)***

<!-- synonyms: 컬럼 상태 복원, 레이아웃 복원, 컬럼 순서 복원, 너비 복원, 숨김 복원, 사용자 개인화 복원, 그리드 레이아웃 저장 복원, 입력한 시트 정보가 올바르지 않습니다, restore column layout, set current info, column state restore -->

> [getCurrentInfo](./get-current-info)로 추출한 컬럼 정보 문자열을 통해 현재 시트의 컬럼 상태(순서, 너비, 숨김 등)를 복원하는 메소드입니다.

### Syntax
```javascript
boolean setCurrentInfo( info );
```

### Parameters
|Name|Type|Required|Description|
|----------|-----|---|----|
|info |`string`|<span class='required'>필수</span>|[getCurrentInfo](./get-current-info)에서 추출한 컬럼 정보 문자열|

### Return Value
***boolean*** : 성공 시 `true`, 실패 시 `false`

### 참고

> `setCurrentInfo`에 넣는 값(저장 시점의 정보)의 **컬럼 `Name` 목록이 현재 시트 `Cols`의 `Name`과 다르면**(그 사이 컬럼을 추가하거나 삭제하거나 이름을 변경한 경우) 복원할 수 없어 `"입력한 시트 정보가 올바르지 않습니다."` 경고가 표시됩니다.   
> 이 경우 기존 저장 정보를 삭제하고 현재 컬럼 기준으로 다시 저장해야 합니다.  
> 반면 컬럼 **너비, 순서, 숨김 변경**이나 `Name`이 동일한 상태의 **Type 변경**은 정상적으로 복원됩니다. 즉 복원 여부는 **컬럼 `Name` 목록이 동일한지**로 결정됩니다.

### Example
```javascript
// getCurrentInfo에서 추출한 문자열로 시트 컬럼 상태를 복원
var info = sheet.getCurrentInfo();
sheet.setCurrentInfo(info);
```

```javascript
// 서버에 저장된 레이아웃을 시트 생성 완료 후 복원
var OPTS = {
    Events: {
        onRenderFirstFinish: function(evtParam) {
            $.ajax({
                url: "/api/layout/load",
                data: { userId: userId },
                success: function(data) {
                    if (data.layoutInfo) {
                        evtParam.sheet.setCurrentInfo(data.layoutInfo);
                    }
                }
            });
        }
    }
};
```

```javascript
// [응용] 복원 전 호환성 확인 — 저장값과 현재 컬럼(Name 목록)이 다르면 setCurrentInfo를 건너뛰어 경고창을 사전에 회피
// 참고: CurrentInfo의 내부 JSON 구조([[LeftCols, Cols, RightCols], ...])에 의존 (getCurrentInfo 반환 구조 참조)
function isSameColStructure(infoA, infoB) {
    function colNames(info) {
        try {
            var parsed = (typeof info === "string") ? JSON.parse(info) : info;
            var groups = parsed[0];   // [LeftCols, Cols, RightCols]
            var names = [];
            for (var i = 0; i < groups.length; i++) names = names.concat(groups[i]);
            return names;             // 순서 무관, 이름 집합만 비교
        } catch (e) { return null; }
    }
    var a = colNames(infoA), b = colNames(infoB);
    if (!a || !b || a.length !== b.length) return false;
    var set = {};
    for (var i = 0; i < a.length; i++) set[a[i]] = true;
    for (var j = 0; j < b.length; j++) if (!set[b[j]]) return false;
    return true;
}

var saved = loadSavedLayout();   // 서버/스토리지에서 불러온, 이전에 저장한 정보 문자열
if (isSameColStructure(saved, sheet.getCurrentInfo())) {
    sheet.setCurrentInfo(saved);  // 컬럼 Name 목록 동일 → 안전하게 복원
} else {
    // 컬럼이 추가/삭제되었거나 이름이 바뀜 → 복원을 건너뛰거나 getCurrentInfo로 재저장
}
```

### Read More
- [getCurrentInfo method](./get-current-info)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
