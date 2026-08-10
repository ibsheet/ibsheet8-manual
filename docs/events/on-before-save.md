# onBeforeSave ***(event)***

<!-- synonyms: onBeforeSave, on-before-save, 저장 직전, 저장 전 이벤트, 데이터 수집 후, doSave 전, 서버 전송 전, 저장 검증, before save, save event, before submit -->

> [doSave](/docs/funcs/core/do-save) 호출 후 전송할 데이터를 수집한 시점에 발생하는 이벤트입니다.  
> [onValidation](./on-validation) 이후, 서버 호출 직전에 발생합니다.  
> `1(true)`를 리턴하면 저장 작업을 중단합니다.

### Syntax
```javascript
options.Events = {
    onBeforeSave: function(evtParam) {

    }
};

// 또는
sheet.bind("onBeforeSave", function(evtParam) {});
```

### Parameters

| Name | Type | Description |
|----------|-----|-------|
|sheet|`object`|변경된 데이터를 가지는 시트 객체|
|source|`object`|시트에 설정된 속성들이 담긴 객체|
|source.params|`string`|서버에 전송할 데이터 변경 사항. querystring 문자열 ([doSave](/docs/funcs/core/do-save) 사용시 `queryMode: 1, 2` 에서 사용가능)|
|source.data|`string`|서버에 전송할 데이터 변경 사항. json 문자열 ([doSave](/docs/funcs/core/do-save) 사용시 `queryMode: 0` 에서 사용가능)|

### Return
***boolean***

### Example
```javascript
options.Events = {
    onBeforeSave: function(evtParam) {
        // 서버에 보낼 데이터가 금지어1 또는 금지어2를 포함하는 경우 Ajax 통신을 실행하지 않습니다.
        if (evtParam.source.params.indexOf("금지어1") > -1 || evtParam.source.params.indexOf("금지어2") > -1) {
            return true;
        }
    }
}
```

```javascript
// 개별 시트에서 대기 이미지 처리 (jQuery BlockUI 사용 예시)
// onBeforeSave에서 표시하고 onAfterSave에서 닫음 — 검증 실패/저장 중단 시 자동으로 안전 (둘 다 미발생)
options.Events = {
    onBeforeSave: function(evtParam) {
        $.blockUI();
    }
}

// ibsheet-common.js에서 공통 대기 이미지 처리 (jQuery BlockUI 사용 예시)
IBSheet.onBeforeCreate = function(obj) {
    var options = obj.options;
    options.Events = options.Events || {};

    // 기존 화면에 설정된 이벤트를 담아둠
    var origBefore = options.Events.onBeforeSave;
    // 공통 이벤트를 먼저 실행하고, 이후 화면단의 이벤트를 실행
    options.Events.onBeforeSave = function(evtParam) {
        $.blockUI();
        if (origBefore) return origBefore(evtParam);
    };

    var origAfter = options.Events.onAfterSave;
    options.Events.onAfterSave = function(evtParam) {
        $.unblockUI();
        if (origAfter) origAfter(evtParam);
    };

    return obj;
};
```

### Read More
- [doSave method](/docs/funcs/core/do-save)
- [저장 응답 규격](/docs/dataStructure/saving-structure)
- [onValidation event](./on-validation)
- [onSave event](./on-save)
- [onAfterSave event](./on-after-save)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.0.0.19|`source.data` 추가|
