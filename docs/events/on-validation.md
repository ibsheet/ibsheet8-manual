# onValidation ***(event)***

<!-- synonyms: 유효성 검사, 사용자 검증, validation, 업무 로직 검사 -->

> [doSave](/docs/funcs/core/do-save), [getSaveJson](/docs/funcs/core/get-save-json), [getSaveString](/docs/funcs/core/get-save-string) 등 저장 API 호출 시 셀별로 순회하며 발생하는 사용자 정의 유효성 검사 이벤트입니다.  
> `doSave`에서는 [onSave](./on-save) 다음에 발생하며, `getSaveJson`/`getSaveString`에서는 이 이벤트만 발생합니다.  
> 셀 순회는 **컬럼 단위로 진행**됩니다 (첫 컬럼의 모든 행 → 다음 컬럼의 모든 행 순서).  
> 필수입력 등 시스템 정의 검사(`validRequired`, `validSize`, `validEditMask`, `validResultMask`)와 별개로, 업무 로직에 따른 검증을 처리합니다.  
> 유효성 검사 기준에 맞지 않으면 `true`를 리턴하여 진행 중인 저장을 중단할 수 있습니다.

### Syntax

```javascript
options.Events = {
    onValidation: function(evtParam) {

    }
};

// 또는
sheet.bind("onValidation", function(evtParam) {});
```

### Parameters
| Name | Type | Description |
|----------|-----|-------|
|sheet|`object`|현재 유효성 검사가 진행되고 있는 시트 객체|
|row|`object`|현재 유효성 검사가 진행되고 있는 셀의 [데이터 로우 객체](/docs/appx/row-object)|
|col|`string`|현재 유효성 검사가 진행되고 있는 셀의 열 이름|

### Return
***boolean***


### Example
```javascript
// 컬럼별로 다른 검증 로직 적용 (공통 헬퍼 사용)
options.Events = {
    onValidation: function(evtParam) {
        var sheet = evtParam.sheet;
        var row = evtParam.row;
        var col = evtParam.col;

        // 검증 대상이 아닌 컬럼은 즉시 통과 (불필요한 if 분기 실행 방지)
        if (col !== "Amount" && col !== "StartDate") return;

        var value = sheet.getValue(row, col);

        // 공통 헬퍼: 메시지 표시 + OK 시 문제 셀로 편집모드 진입 + 저장 중단 신호
        function alertAndFocus(msg) {
            sheet.showMessageTime({
                message: msg,
                buttons: ["OK"],
                func: function() {
                    // sheet.focus(row, col);    // 포커스만 (편집모드 진입 X)
                    sheet.startEdit(row, col);   // 포커스 + 편집모드 진입
                }
            });
            return true;
        }

        // Amount 컬럼: 0 이상이어야 함
        if (col === "Amount" && value < 0) {
            return alertAndFocus("Amount는 0 이상이어야 합니다.");
        }

        // StartDate 컬럼: 같은 행의 EndDate보다 이전이어야 함
        if (col === "StartDate") {
            var endDate = sheet.getValue(row, "EndDate");
            if (endDate && value > endDate) {
                return alertAndFocus("시작일은 종료일보다 이전이어야 합니다.");
            }
        }
    }
}
```

### Read More
- [doSave method](/docs/funcs/core/do-save)
- [getSaveJson method](/docs/funcs/core/get-save-json)
- [getSaveString method](/docs/funcs/core/get-save-string)
- [저장 응답 규격](/docs/dataStructure/saving-structure)
- [onSave event](./on-save)
- [onBeforeSave event](./on-before-save)
- [onAfterSave event](./on-after-save)

### Since

|product|version|desc|
|---|---|---|
|core|8.2.0.19|기능 추가|
