# Timeout ***(cfg)***

<!-- synonyms: Timeout, ajax timeout, server timeout, request timeout, connection timeout, 타임아웃, 서버 통신 타임아웃, 서버 요청 타임아웃, ajax 타임아웃, doSave timeout, 서버 대기 시간 -->

> 시트에서 사용되는 조회, 저장 등 Ajax 통신(`ajax`, `doSave`, `doSearch`, `doSearchPaging`)의 최대 대기 시간 값을 설정합니다.  
> 입력 값은 `초(second)` 단위이며, 기본값은 `60초`입니다.  
> **각 함수 호출 시 `timeout` 인자를 직접 지정하면 그 인자 값이 우선 적용되고, 지정하지 않은 호출에만 이 `Cfg.Timeout` 기본값이 사용됩니다.**  
> 서버(WAS)의 연결 타임아웃이 이 값보다 짧으면 서버에서 먼저 연결이 종료될 수 있습니다.  
> 타임아웃이 발생하면 화면에 `연결시간이 초과됐습니다.` 메시지(메시지 파일 `ko.js`/`en.js`의 `ResultErrRequestTimeout`)를 표시하고 대기를 멈출 뿐, 서버에서 진행 중인 요청은 중단되지 않습니다.  
> 단, 엑셀과 텍스트 파일 다운로드/업로드에는 적용되지 않습니다.

### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`number`|서버 통신 최대 대기 시간(초 단위). 기본값 `60`|

### Example
```javascript
options = {
    Cfg :{
        Timeout: 120,  // 최대 대기 시간을 120초(2분)로 설정
        ...
    }
};
```

### Read More
- [ajax method](/docs/funcs/core/ajax)
- [doSave method](/docs/funcs/core/do-save)
- [doSearch method](/docs/funcs/core/do-search)
- [doSearchPaging method](/docs/funcs/core/do-search-paging)
- [onBeforeDataLoad event](/docs/events/on-before-data-load)
- [down2Excel method](/docs/funcs/excel/down-to-excel)
- [loadExcel method](/docs/funcs/excel/load-excel)
- [엑셀파일 업로드/다운로드 appendix](/docs/appx/import-export)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.5|기능 추가|
