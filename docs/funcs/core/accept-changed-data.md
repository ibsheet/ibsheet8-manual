# acceptChangedData ***(method)***

<!-- synonyms: 변경 반영, 상태 초기화, 저장 후 처리, accept changed, 시트 상태 클리어 -->

> 시트 내에 변경된 내용(입력, 수정, 삭제)을 적용 합니다.  
> 행의 상태가 `Added(입력)`, `Changed(수정)`인 행은 상태만 클리어되고, `Deleted(삭제)`인 행은 제거됩니다.  
> 주로 서버 저장 처리 후, `IO.Result`가 성공(`Result >= 0`)인 경우 시트 상태를 초기화할 때 사용합니다.  
> 인자로 [데이터 로우 객체](/docs/appx/row-object)를 지정하면 해당 행에 대해서만 적용 합니다.  
> **주의**: `acceptChangedData`는 [onAfterSave](/docs/events/on-after-save) 이벤트를 발생시키지 않으며, 단순히 시트 상태를 초기화합니다.


### Syntax
```javascript
void acceptChangedData( row );
```

### Parameters

|Name|Type|Required|Description|
|----------|-----|---|----|
|row|`object`|<span class='optional'>선택</span>|[데이터 로우 객체](/docs/appx/row-object)|


### Return Value
***none***


### Example
```javascript
// ajax 저장 성공 후 시트 상태 클리어 (서버 응답을 직접 처리하는 경우)
$.ajax({
    type: 'post',
    url: '/save.do',
    dataType: 'json',
    data: JSON.stringify(saveJson),
    success: function(data) {
        if (data.IO.Result >= 0) {
            sheet.acceptChangedData();   // 상태 초기화 (onAfterSave 발생 안 함)
        } else {
            alert(data.IO.Message);
        }
    }
});

// 특정 행만 클리어
sheet.acceptChangedData(sheet.getRowById('AR4'));
```

### Read More
- [dataStructure](/docs/dataStructure/saving-structure)
- [applySaveResult method](./apply-save-result)
- [doSave method](./do-save)
- [getSaveJson method](./get-save-json)
- [getSaveString method](./get-save-string)
- [hasChangedData method](./has-changed-data)
- [getChangedData method](./get-changed-data)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
