# setCurrentInfo ***(method)***
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

> 저장 이후 시트의 컬럼 정의(`Cols`)가 변경되면(예: 컬럼 추가/삭제/이름 변경) 복원할 수 없습니다. `"입력한 시트 정보가 올바르지 않습니다."` 경고가 표시되며, 기존 저장 정보를 삭제하고 다시 저장해야 합니다.

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

### Read More
- [getCurrentInfo method](./get-current-info)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
