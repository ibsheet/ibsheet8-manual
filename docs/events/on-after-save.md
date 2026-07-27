# onAfterSave ***(event)***

<!-- synonyms: 저장 완료, 저장 후, after save, save response -->

> 저장 처리가 완료된 후 발생하는 이벤트입니다 (성공/실패 모두).  
> [doSave](/docs/funcs/core/do-save) 호출 시 서버 응답 수신 후 자동 발생하며, [applySaveResult](/docs/funcs/core/apply-save-result)를 직접 호출해도 발생합니다.  
> `1(true)`를 리턴하면 저장 실패 시(시스템 오류 또는 사용자 정의 오류) 시트에 자동으로 표시되는 오류 메시지 출력을 막을 수 있습니다.

### Syntax
```javascript
options.Events = {
    onAfterSave: function(evtParam) {

    }
};

// 또는
sheet.bind("onAfterSave", function(evtParam) {});
```

### Parameters
| Name | Type | Description |
|----------|-----|-------|
|sheet|`object`|서버에 변경된 내용을 전송한 시트 객체|
|result |`number`|**서버 응답 결과 코드**<br/>`0`:성공, `-3`/`-5`/`-6`/`-7`:시스템 오류, 그 외:사용자 정의<br/>상세는 [저장 응답 규격](/docs/dataStructure/saving-structure)을 참고|
|message|`string`|서버에서 전달 받은 메시지|
|response|`object`|서버 응답 객체(XMLHttpRequest 객체)|

### Return
***boolean***

### Example
```javascript
options.Events = {
    onAfterSave: function(evtParam) {
        // 서버 응답이 '성공'인 경우
        if (evtParam.result == 0) {
            evtParam.sheet.showMessageTime({message: "성공적으로 저장되었습니다.", time: 1000});
        }
    }
}
```

```javascript
// 개별 시트에서 대기 이미지 닫기 (jQuery BlockUI 사용 예시)
// onBeforeSave에서 표시한 대기 이미지를 응답 수신 후 닫습니다.
options.Events = {
    onAfterSave: function(evtParam) {
        $.unblockUI();
    }
}

// ibsheet-common.js에서 공통 대기 이미지 처리 (jQuery BlockUI 사용 예시)
IBSheet.onBeforeCreate = function(obj) {
    var options = obj.options;
    options.Events = options.Events || {};

    var origBefore = options.Events.onBeforeSave;
    options.Events.onBeforeSave = function(evtParam) {
        $.blockUI();
        if (origBefore) return origBefore(evtParam);
    };

    var origAfter = options.Events.onAfterSave;
    options.Events.onAfterSave = function(evtParam) {
        $.unblockUI();
        if (origAfter) return origAfter(evtParam);
    };

    return obj;
};
```

### Read More

- [doSave method](/docs/funcs/core/do-save)
- [저장 응답 규격](/docs/dataStructure/saving-structure)
- [onValidation event](./on-validation)
- [onSave event](./on-save)
- [onBeforeSave event](./on-before-save)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.0.0.17|`return` 동작 추가|
