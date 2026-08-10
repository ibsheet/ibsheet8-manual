# XlsImportMode ***(cfg)***

<!-- synonyms: XlsImportMode, xls import mode, xls upload server, importData xls, xls server module, xls 업로드 서버, xls 서버 모듈, xls 파일 업로드 방식, xls 파일 클라이언트 서버 -->

> importData() 함수를 사용할 때, 파일선택창에서 xls 파일 선택시 서버모듈로 전환할지 여부를 결정합니다. 

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|클라이언트 모듈을 사용합니다. (`default`)|
|`1(true)`|서버 모듈을 사용합니다.|

### Example
```javascript
options.Cfg = {
    XlsImportMode: 1
};

// 파일 선택창에서 xls 파일 선택시 자동으로 서버모듈로 전환합니다.
sheet.importData();
```

### Read More
- [importData method](/docs/funcs/core/import-data)
- [loadExcel method](/docs/funcs/excel/load-excel)

### Since

|product|version|desc|
|---|---|---|
|excel|8.2.0.16|기능 추가|
