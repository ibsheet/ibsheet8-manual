# showFixedRows ***(method)***

<!-- synonyms: showFixedRows, show-fixed-rows, 고정행, 헤드, 푸터, Head, Foot, 고정, 생성, 표시, fixed, rows, header, footer -->

> `Head` 행, `Foot` 행을 생성합니다.  
> 인자로 전달하는 `Head`/`Foot` 행 객체의 구조는 [Head / Foot appendix](/docs/appx/head-foot) 를 참고해주세요.  
> 각 행 객체의 `Kind`(행의 **종류**)에 `"Head"` 또는 `"Foot"`을 지정해 어떤 고정행을 만들지 정합니다. → [Kind appendix](/docs/appx/kind)


### Syntax
```javascript
boolean showFixedRows( fixedobject );
```

### Parameters
|Name|Type|Required| Description |
|----------|-----|---|----|
|fixedobject |`array[object]`|<span class='required'>필수</span>|객체를 배열로 감싸서 전달.<br/> 각 객체에 `Kind`(행 종류) 필수 — `"Head"` 또는 `"Foot"`|


### Return Value
***boolean*** : `Head` 행 `Foot` 행 생성 여부 (잘못된 인자 값에 의해 수행되지 못하는 경우 `0(false)` 리턴)

### Example
```javascript
// 1. Head 행 1개, Foot 행 1개 생성
var obj1 = [{Kind : 'Head', ... },{Kind : 'Foot', ... }];
sheet.showFixedRows(obj1);

// 2. Cols 속성을 상속받지 않는 Foot 행 생성
// Foot 행은 Cols의 Type, Format 등의 속성을 상속받아 원치 않는 내용이 표시될 수 있습니다.
// 각 컬럼의 속성을 직접 지정하여 이를 방지할 수 있습니다.
// onRenderFirstFinish 이벤트에서 Foot 행을 생성하고, onSearchFinish에서 값을 세팅합니다.

// 2-1. 컬럼별로 직접 지정하는 방식
var OPTS = {
    Cols: [
        { Header: "상품명", Name: "prodName", Type: "Text", Width: 150 },
        { Header: "수량", Name: "qty", Type: "Int", Width: 80 },
        { Header: "납품일", Name: "delivDate", Type: "Date", Format: "yyyy-MM-dd", Width: 100 }
    ],
    Events: {
        onRenderFirstFinish: function(evtParam) {
            evtParam.sheet.showFixedRows([{
                Kind: "Foot",
                id: "myFootRow",
                prodName: { Type: "Text", Value: "합계", CanEdit: 0 },
                qty: { Type: "Int", Format: "#,###", Value: 0, CanEdit: 0, EmptyValue: "" },
                delivDate: { Type: "Text", Value: "", CanEdit: 0, EmptyValue: "" }
            }]);
        },
        onSearchFinish: function(evtParam) {
            // serverTotal: 서버에서 조회한 전체 합계값
            evtParam.sheet.setValue(evtParam.sheet.getRowById("myFootRow"), "qty", serverTotal);
        }
    }
};

// 2-2. 컬럼이 많은 경우 Cols를 순회하여 자동 생성
var options = {
    Events: {
        onRenderFirstFinish: function(evtParam) {
            var footRow = { Kind: "Foot", id: "myFootRow" };
            var allCols = (options.LeftCols || []).concat(options.Cols || []).concat(options.RightCols || []);

            allCols.forEach(function(col) {
                var type = (col.Type === "Int" || col.Type === "Float") ? col.Type : "Text";
                footRow[col.Name] = { Type: type, Value: "", CanEdit: 0, EmptyValue: "" };
            });

            evtParam.sheet.showFixedRows([footRow]);
        },
        onSearchFinish: function(evtParam) {
            // serverTotal: 서버에서 조회한 전체 합계값
            evtParam.sheet.setValue(evtParam.sheet.getRowById("myFootRow"), "qty", serverTotal);
        }
    }
};
// 3. onBeforeCreate에서 공통으로 Foot 행 추가
// 모든 시트에 공통으로 Foot 행을 추가하려면 onBeforeCreate에서 처리합니다.
// ibsheet-common.js에 추가하면 모든 페이지에서 적용됩니다.
IBSheet.onBeforeCreate = function(obj) {
    var options = obj.options;
    var mode = options.Cfg && options.Cfg.SearchMode;

    // 서버 페이징(3,4,5)인 경우 공통 Foot 행 생성
    if (mode >= 3 && mode <= 5) {
        // 기존 화면에 설정된 이벤트를 담아둠
        var origRender = options.Events && options.Events.onRenderFirstFinish;
        options.Events = options.Events || {};
        // 공통 이벤트를 먼저 실행하고, 이후 화면단의 이벤트를 실행
        options.Events.onRenderFirstFinish = function(evtParam) {
            var footRow = { Kind: "Foot", id: "myFootRow" };
            var allCols = (options.LeftCols || []).concat(options.Cols || []).concat(options.RightCols || []);

            allCols.forEach(function(col) {
                var type = (col.Type === "Int" || col.Type === "Float") ? col.Type : "Text";
                footRow[col.Name] = { Type: type, Value: "", CanEdit: 0, EmptyValue: "" };
            });

            evtParam.sheet.showFixedRows([footRow]);
            if (origRender) origRender(evtParam);
        };
    }

    return obj;
};
```

### Read More
- [Head / Foot appendix](/docs/appx/head-foot)
- [SearchMode cfg](/docs/props/cfg/search-mode)
- [행(Row) 구조](/docs/start/row)
- [setValue method](/docs/funcs/core/set-value)
- [onRenderFirstFinish event](/docs/events/on-render-first-finish)
- [onBeforeCreate static](/docs/static/on-before-create)

### Since

|product|version|desc|
|---|---|---|
|core|8.2.0.4|기능 추가|
