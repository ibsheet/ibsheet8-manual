# onExportFinish ***(event)***

<!-- synonyms: 다운로드 완료 이벤트, 엑셀 다운로드 완료, export finish, 다운로드 후 -->

> 시트의 내용을 `Excel, Text, Pdf` 등으로 다운로드 하는 함수([down2Excel](/docs/funcs/excel/down-to-excel), [down2Text](/docs/funcs/excel/down-to-text), [exportData](/docs/funcs/core/export-data), [down2Pdf](/docs/funcs/excel/down-to-pdf)) 호출 후 다운로드 완료 시 발생합니다.

### Syntax

```
    onExportFinish : function(paramObject) {

    }
or
    sheet.bind("onExportFinish" , function(paramObject) {});
```

### Parameters


| Name | Type | Description |
|----------|-----|-------|
|sheet|`object`|시트 객체|
|type|`string`|[down2Excel](/docs/funcs/excel/down-to-excel), [down2Text](/docs/funcs/excel/down-to-text), [exportData](/docs/funcs/core/export-data), [down2Pdf](/docs/funcs/excel/down-to-pdf) 함수 호출에 따라 `EXCEL`, `TEXT`, `PDF`|
|result|`boolean`|다운로드 처리 결과<br>`0(false)`:오류 발생<br>`1(true)`:정상 종료|

### Return
***none***

### Example
```javascript
options.Events = {
    onExportFinish:function(evtParam){
        //다운로드 완료 후 메세지 표시
        if(evtParam.result){
            alert("다운로드가 완료 되었습니다.");
        }
    }
}
```

### Read More
- [엑셀 다운로드 이벤트 발생 순서](/docs/events/12-excel-down-event-flow)
- [exportData method](/docs/funcs/core/export-data)
- [down2Excel method](/docs/funcs/excel/down-to-excel)
- [down2Text method](/docs/funcs/excel/down-to-text)
- [onBeforeExport event](./on-before-export)

### Since

|product|version|desc|
|---|---|---|
|excel|0.0.0|기능 추가|
