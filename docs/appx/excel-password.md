# 엑셀 비밀번호 설정 ***(appendix)***

<!-- synonyms: 엑셀 비밀번호, 엑셀 암호, workbookPassword, 엑셀 파일 암호화, password protect excel, 비밀번호 엑셀 다운로드, 암호 엑셀 업로드, 암호 걸린 엑셀 -->

> 엑셀 파일에 비밀번호(암호)를 설정하거나, 비밀번호가 걸린 엑셀을 읽는 방법입니다.  
> 서버 모듈([down2Excel](/docs/funcs/excel/down-to-excel) / [loadExcel](/docs/funcs/excel/load-excel))과 클라이언트 모듈([exportData](/docs/funcs/core/export-data) / [importData](/docs/funcs/core/import-data))의 지원 방식이 다릅니다.

## 서버 모듈 — `workbookPassword`

`down2Excel`(다운로드)과 `loadExcel`(업로드)은 `workbookPassword` 옵션을 기본 제공합니다. **xlsx 확장자에서만** 지원됩니다.

```javascript
// 다운로드: 비밀번호가 걸린 xlsx 생성
sheet.down2Excel({ fileName: "list.xlsx", workbookPassword: "1234" });

// 업로드: 비밀번호가 걸린 xlsx 읽기
sheet.loadExcel({ workbookPassword: "1234" });
```

비밀번호가 틀린 경우 [onImportFinish](/docs/events/on-import-finish) 이벤트의 `result` 코드로 확인합니다.

## 클라이언트 모듈 — 외부 라이브러리 사용

`exportData` / `importData`는 비밀번호 설정을 **기본 제공하지 않습니다.**   
`xlsx-populate.js` 같은 외부 라이브러리를 활용해 구현하며, `8.3.0.5-20250424-14` 이상에서 지원됩니다.

- **다운로드**: `onBeforeExport` 이벤트에서 전달되는 data로 파일에 암호를 적용하고, `return 1`로 IBSheet 기본 다운로드 동작을 차단한 뒤 보호된 파일을 내려받습니다.
- **업로드**: 파일 선택 UI에서 비밀번호를 적용해 파일을 읽은 뒤 `importData`로 시트에 바인딩합니다.

구현 예제: [exportData passWord 샘플](https://jsfiddle.net/gh/get/library/pure/ibsheet/ibsheet8-manual-sample/tree/master/samples/method/exportData/passWord)

### Read More
- [down2Excel method](/docs/funcs/excel/down-to-excel)
- [loadExcel method](/docs/funcs/excel/load-excel)
- [exportData method](/docs/funcs/core/export-data)
- [importData method](/docs/funcs/core/import-data)
- [onImportFinish event](/docs/events/on-import-finish)
