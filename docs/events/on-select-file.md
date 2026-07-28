# onSelectFile ***(event)***

<!-- synonyms: 파일 선택 이벤트, 엑셀 업로드 전, select file, 업로드 취소 -->

> [importData](/docs/funcs/core/import-data), [loadExcel](/docs/funcs/excel/load-excel), [loadText](/docs/funcs/excel/load-text) 함수를 호출하여 사용자가 엑셀/텍스트 파일을 선택할 때 발생합니다.  
> 위 함수 호출 시 먼저 파일 선택 창이 열리고, 여기서 파일을 선택했을 때 발생합니다.  
> 해당 이벤트에서 `false`를 리턴할 경우 파일 업로드가 취소됩니다.

### Syntax

```
    onSelectFile : function(paramObject) {

    }
or
    sheet.bind("onSelectFile" , function(paramObject) {});
```

### Parameters


| Name | Type | Description |
|----------|-----|-------|
|sheet|`object`|시트 객체|
|type|`string`|[importData](/docs/funcs/core/import-data), [loadExcel](/docs/funcs/excel/load-excel), [loadText](/docs/funcs/excel/load-text) 함수 호출에 따라 `EXCEL`, `TEXT`|
|filename|`string`|선택한 파일 명|

### Return
***boolean***  
`false`를 리턴하면 파일 업로드가 취소됩니다.

### Example
```javascript
options.Events = {
    onSelectFile:function(evtParam){
       //업로드 완료시까지 화면에 block을 띄운다.
       $.blockUI({ message: '<h1><img src="busy.gif" />파일 업로드 작업중입니다...</h1>' });
    }
}
```

### Read More
- [엑셀 업로드 이벤트 발생 순서](/docs/events/13-excel-up-event-flow)
- [importData method](/docs/funcs/core/import-data)
- [loadExcel method](/docs/funcs/excel/load-excel)
- [loadText method](/docs/funcs/excel/load-text)
- [onImportFinish event](./on-import-finish)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
