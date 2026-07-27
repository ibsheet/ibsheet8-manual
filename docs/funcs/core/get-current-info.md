# getCurrentInfo ***(method)***
> 현재 시트의 컬럼 정보를 **문자열로 반환**합니다. 반환된 값을 서버 등에 직접 저장하여 활용할 수 있습니다.  
> 사용자가 컬럼을 숨기거나, 이동하거나, 사이즈를 조절한 상태를 추출할 수 있습니다.  
> 반환된 문자열을 [setCurrentInfo](./set-current-info)에 전달하면 시트의 컬럼 상태를 복원할 수 있습니다.

### Syntax
```javascript
string getCurrentInfo();
```

### Return Value
***string*** : 현재 컬럼들의 숨김, 너비, 위치 정보를 담은 문자열

반환 문자열은 다음과 같은 구조입니다:
```
// 일반 시트
[컬럼순서배열, 컬럼속성객체, sort정보, null]

// 멀티레코드 시트
[컬럼순서배열, 컬럼속성객체, sort정보, {}]
```


```javascript
// 반환 예시
'[
  [["SEQ"],["TextData","LinesData","ComboData","ISO","IntData","FloatData","DateData","LinkData","ImageData"],["PassData","RadioData","CheckData"]],
  {
    "SEQ":{"Visible":1,"Width":50,"RelWidth":0,"UserHidden":false},
    "TextData":{"Visible":0,"Width":100,"RelWidth":0,"UserHidden":false,"Hidden":1},
    "LinesData":{"Visible":0,"Width":250,"RelWidth":1,"UserHidden":false,"Hidden":1},
    "ComboData":{"Visible":1,"Width":100,"RelWidth":0,"UserHidden":false},
    "IntData":{"Visible":1,"Width":80,"RelWidth":0,"UserHidden":false},
    ...
  },"-LinesData,TextData",null
]'
```

| 구성 요소 | 설명 |
|-----------|------|
| 컬럼순서배열 | `[[고정 좌측열(LeftCols)], [비고정 열(Cols)], [고정 우측열(RightCols)]]` — 컬럼의 현재 순서 |
| 컬럼속성객체 | 각 컬럼별 속성 정보 (아래 표 참조) |
| 현재sort정보 | 현재 시트에 적용된 `sort` 정보  |

| 속성 | 설명 |
|------|------|
| `Visible` | 열 보임 여부 (`true(1)`: 보임, `false(0)`: 숨김) |
| `Width` | 열 너비 (px) |
| `RelWidth` | 상대 너비 비율 |
| `Hidden` | 열 숨김 여부 (`1`: 숨김). [Col.Visible](/docs/props/col/visible)을 `0`으로 설정하거나 [hideCol](./hide-col)로 숨긴 경우 `1`로 표시됨 |
| `UserHidden` | [hideCol](./hide-col)의 `userHidden` 인자를 `1`로 설정하여 숨긴 열 여부 (`1`: 사용자 숨김, `0`: 아님). `UserHidden:1`이면 `Hidden`도 함께 `1`이 됨 |

### Example
```javascript
// 사용자별 컬럼 레이아웃을 서버에 저장
function saveLayout() {
    var info = sheet.getCurrentInfo();
    $.ajax({
        url: "/api/layout/save",
        type: "POST",
        data: { userId: userId, layoutInfo: info },
        success: function() {
            alert("레이아웃이 저장되었습니다.");
        }
    });
}

// 시트 생성 완료 후 저장된 레이아웃 복원
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
// 초기화 버튼 — 시트 생성 시 초기 상태를 저장해두고 원래대로 복원
var initInfo = null;

var OPTS = {
    Events: {
        onRenderFirstFinish: function(evtParam) {
            if (!initInfo) {
                initInfo = evtParam.sheet.getCurrentInfo();
            }
        }
    }
};

// 초기화 버튼 클릭 시 복원
document.getElementById("btnReset").onclick = function() {
    if (initInfo) {
        sheet.setCurrentInfo(initInfo);
    }
};
```

### Read More
- [setCurrentInfo method](./set-current-info)
- [hideCol method](./hide-col)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
