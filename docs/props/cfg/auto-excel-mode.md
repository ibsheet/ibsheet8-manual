# AutoExcelMode ***(cfg)***

<!-- synonyms: excel mode, server excel, client excel export, auto excel module, 엑셀 모듈 분기, 엑셀 모드 -->

> `down2Excel()` 또는 `loadExcel()` 호출 시 서버 모듈로 처리할지, 클라이언트 모듈로 분기할지를 설정합니다.  
> 개발자는 동일하게 `down2Excel`, `loadExcel`을 호출하며 이 옵션 값에 따라 내부 처리 방식이 결정됩니다.

- **서버 모듈**: 백엔드를 통해 엑셀 다운로드/업로드 수행 (`down2Excel`, `loadExcel`)
- **클라이언트 모듈**: 브라우저에서 직접 엑셀 다운로드/업로드 수행 (`exportData`, `importData`)

### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`1`|서버 모듈 사용 (`down2Excel`, `loadExcel`) (`default`)|
|`2`|클라이언트 모듈 사용 (`exportData`, `importData`) — IE10 이상에서 지원|
|`3`|브라우저 성능 기준 자동 선택. IE9 이하: 서버 모듈 / IE10 이상 또는 모던 브라우저: 클라이언트 모듈|

### Example
```javascript
// 1. 클라이언트 모듈 강제 사용
options = {
  Cfg: {
    AutoExcelMode: 2
  }
};

// down2Excel 호출 시 내부적으로 클라이언트 모듈(exportData)로 처리
sheet.down2Excel({ fileName: "Excel.xlsx" });

// 2. 자동 분기
options = {
  Cfg: {
    AutoExcelMode: 3
  }
};

// 브라우저 환경에 따라 서버/클라이언트 모듈 자동 선택
sheet.loadExcel();
```

### Read More
- [down2Excel method](/docs/funcs/excel/down-to-excel)
- [loadExcel method](/docs/funcs/excel/load-excel)
- [exportData method](/docs/funcs/core/export-data)
- [importData method](/docs/funcs/core/import-data)
- [SuppressExportMessage cfg](./suppress-export-message)

### Since

|product|version|desc|
|---|---|---|
|excel|8.0.0.4|기능 추가|
|excel|8.0.0.5|명칭 변경 `ExportMode => AutoExcelMode`|
