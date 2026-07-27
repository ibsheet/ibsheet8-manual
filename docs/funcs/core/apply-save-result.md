# applySaveResult ***(method)***

<!-- synonyms: 저장 결과 반영, 서버 응답 처리, 저장 응답 적용, save result, apply save -->

> 서버에 저장한 후 반환된 결과를 기반으로 시트의 수정 내용을 처리합니다.  
> **성공** 응답(`Result >= 0`)인 경우, [acceptChangedData](./accept-changed-data)를 통해 상태를 초기화 합니다.  
> **실패** 응답(`Result < 0`)인 경우, 값에 따라 경고 메세지를 표시합니다.


### Syntax
```javascript
boolean applySaveResult( result, message, response, files );
```

### Parameters
|Name|Type|Required|Description|
|----------|-----|---|----|
|result|`number`|<span class='required'>필수</span>|서버 응답 결과([onAfterSave](/docs/events/on-after-save) 이벤트의 `result` 파라미터 값 참고.)|
|message|`string`|<span class='optional'>선택</span>|[onAfterSave](/docs/events/on-after-save) 이벤트로 전달할 메세지 문자열|
|response|`object`|<span class='optional'>선택</span>|ajax 통신의 response 객체([onAfterSave](/docs/events/on-after-save) 이벤트로 전달)|
|files|`array`|<span class='optional'>선택</span>|`file` 타입 저장 시 ajax 통신 후 저장된 파일 데이터를 전달 ([getSaveJson](./get-save-json)의 `formData`인자와 함께 사용)|


### Return Value
***boolean*** : 함수 정상 동작 여부. (인자값이 잘못되어 수행되지 못한 경우에는 `false` 리턴)

### Example
```javascript
// IBSheet 표준 저장 응답 규격을 그대로 활용
$.ajax({
    type: 'post',
    url: '/save.do',
    dataType: 'json',
    data: JSON.stringify(saveJson),
    success: function(data) {
        // applySaveResult가 내부적으로 acceptChangedData 호출 + onAfterSave 발생
        sheet.applySaveResult(data.IO.Result, data.IO.Message, data);
    }
});

// 후처리는 onAfterSave 이벤트에서 처리 (성공/실패 분기, UI 업데이트 등)
options.Events = {
    onAfterSave: function(evtParam) {
        if (evtParam.result >= 0) {
            // 정상 저장 후 처리 (예: 새로고침)
        } else {
            // 실패 후 처리 (실패 메시지는 IBSheet가 자동 표시)
        }
    }
};
```

### Read More
- [dataStructure](/docs/dataStructure/saving-structure)
- [acceptChangedData method](./accept-changed-data)
- [doSave method](./do-save)
- [getSaveJson method](./get-save-json)
- [getSaveString method](./get-save-string)
- [onAfterSave event](/docs/events/on-after-save)
- [Required col](/docs/props/col/required)
- [ValidateMessage cfg](/docs/props/cfg/validate-message)
- [ValidCheck cfg](/docs/props/cfg/valid-check)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.0.0.5|files 기능 추가|