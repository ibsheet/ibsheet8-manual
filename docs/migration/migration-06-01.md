# Status 타입 마이그레이션

<!-- synonyms: IBSheet7, 마이그레이션, sheet7, migration, v7, v8, ibsheet7에서 ibsheet8로, Status 타입, Status 컬럼, Status column, 상태 컬럼, DelCheck, Deleted, Added -->

ibsheet7의 `Status` 타입은 ibsheet8에 없고, 행 추가/삭제/수정 시 자동으로 관리됩니다 (행 객체에 `Added`, `Deleted`, `Changed` 속성 추가).  
상태에 따라 행 색상도 자동 변경됩니다 (파랑: 신규, 분홍: 삭제, 노랑: 수정).

만약 ibsheet7처럼 상태를 보여주는 컬럼을 만들고자 하시는 경우에는 `IBSheet-common.js` 파일에 `IB_Preset.STATUS`를 (Col)[Extend](/docs/props/col/extend)하시면 됩니다.

```javascript
var initSheet = {
    // IB_Preset.STATUS는 내부적으로 Formula를 사용하므로 CanFormula·CalcOrder 필수
    Def: {
        Row: { CanFormula: 1, CalcOrder: "RStatus" }
    },
    Cols:[
        //Status 열처럼 동작하는 열을 만든다.
        {
            Header: "상태",
            Name: "RStatus",
            Extend: IB_Preset.STATUS
        }
    ]
};
```

## 참고

- 위 IB_Preset.STATUS의 내용을 ibsheet-common.js 에 찾아보면 [Formula (col)](/docs/props/col/formula)를 사용하므로 [Def/Row](/docs/start/basic-structure)에 [CanFormula (row)](/docs/props/row/can-formula) 속성이 1로 설정하고 [CalcOrder (row)](/docs/props/row/calc-order) 속성이 설정 되어야 합니다.
- 저장 시 [Formula (col)](/docs/props/col/formula)로 `STATUS` 데이터 값이 변경되므로 `local/언어.js` 파일 안에 문자열(`"ReqStatusAdded": "Added"`(I), `"ReqStatusChanged": "Changed"`(U), `"ReqStatusDeleted": "Deleted"`(D), `"ReqStatusEmpty": ""`(R))을 수정해야 합니다.
- IBSheet7의 `Cfg.ImageStatus` 속성처럼 상태를 별도 이미지로 표시하고자 하는 경우에는 [Format (col)](/docs/props/col/format)에서 입력,수정,삭제 대신 해당 이미지를 넣어 주시면 됩니다.

```js
Format:{"I":"<img src='../images/added.gif'>","U":"<img src='../images/changed.gif'>","D":"..."}
```

## 공통 적용 (onBeforeCreate로 자동 처리)

시트마다 `Def.Row.CanFormula: 1, CalcOrder: "RStatus"`를 넣는 것이 번거로우면, [onBeforeCreate (static)](/docs/static/on-before-create)에서 공통으로 처리할 수 있습니다.  
`IB_Preset.STATUS`처럼 `Formula`를 사용하는 프리셋을 [Extend (col)](/docs/props/col/extend)한 열을 찾아 `CalcOrder`를 자동 주입합니다.  
이렇게 하면 각 시트 옵션에서는 `Extend`만 지정하고 `Def.Row.CanFormula`/`CalcOrder`는 생략할 수 있습니다.

```javascript
// 시트 생성 직전에 호출 (IBSheet.create 인자가 opt.options에 들어있음)
IBSheet.onBeforeCreate = function (opt) {
    var calcCols = [];
    var collect = function (cols) {
        if (!cols) return;
        for (var i = 0; i < cols.length; i++) {
            // Formula를 사용하는 프리셋(IB_Preset.STATUS 등)을 Extend한 열을 수집
            if (cols[i].Extend && cols[i].Extend.Formula) calcCols.push(cols[i].Name);
        }
    };
    collect(opt.options.Cols);
    collect(opt.options.LeftCols);
    collect(opt.options.RightCols);

    if (calcCols.length) {
        opt.options.Def = opt.options.Def || {};
        opt.options.Def.Row = opt.options.Def.Row || {};
        opt.options.Def.Row.CanFormula = 1;
        // 기존 CalcOrder가 있으면 이어붙인다.
        opt.options.Def.Row.CalcOrder = opt.options.Def.Row.CalcOrder
            ? opt.options.Def.Row.CalcOrder + ',' + calcCols.join(',')
            : calcCols.join(',');
    }

    // 반드시 수정된 opt를 리턴해야 시트가 만들어짐
    return opt;
};
```
