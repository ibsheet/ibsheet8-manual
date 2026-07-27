# LoadExcelConfig ***(cfg)***

<!-- synonyms: loadexcel 공통 옵션, 엑셀 업로드 공통 설정, excel upload config, default loadexcel param -->

> [loadExcel](/docs/funcs/excel/load-excel) 함수 호출 시 사용할 기본 인자를 공통으로 설정합니다.  
> [IBSheet.CommonOptions](/docs/static/common-options)의 `Cfg` 속성에 지정하면 모든 시트의 `loadExcel` 호출에 이 설정이 기본값으로 적용됩니다.  
> 시트별로 동일한 속성을 다시 지정하면 시트의 값이 우선합니다.

### Type
`object`

### Options
|Value|Description|
|-----|-----|
|`object`|[loadExcel](/docs/funcs/excel/load-excel) 함수의 인자 객체와 동일한 구조|

### Example
```javascript
options.Cfg = {
  // 모든 화면에서 엑셀 업로드 시 기본 속성을 설정
  LoadExcelConfig: {
    "append": 1,
    "mode": "HeaderSkip"
  }
};
```

### Read More
- [loadExcel method](/docs/funcs/excel/load-excel)
- [Down2ExcelConfig cfg](./down-to-excel-config)
- [AutoExcelMode cfg](./auto-excel-mode)
- [IBSheet.CommonOptions static](/docs/static/common-options)

### Since

|product|version|desc|
|---|---|---|
|excel|0.0.0|기능 추가|
