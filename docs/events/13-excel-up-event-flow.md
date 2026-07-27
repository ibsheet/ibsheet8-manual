# 엑셀 업로드 이벤트 발생 순서 ***(event flow)***

<!-- synonyms: 엑셀 업로드, 엑셀 가져오기, excel upload, import -->

> 업로드 함수([loadExcel](/docs/funcs/excel/load-excel), [importData](/docs/funcs/core/import-data), [loadText](/docs/funcs/excel/load-text)) 호출 시 이벤트 발생 순서입니다.  
> 조회 이벤트와 겹치므로, `type` 파라미터로 엑셀(`EXCEL`)과 조회(`Search`)를 구분할 수 있습니다.

### 발생 순서

[onSelectFile](/docs/events/on-select-file) → 파일 전송/파싱 → [onReceiveData](/docs/events/on-receive-data) → [onImportFinish](/docs/events/on-import-finish) → [onDataLoad](/docs/events/on-data-load) → [onSearchFinish](/docs/events/on-search-finish)

### 이벤트별 시점 및 용도

| 이벤트 | 시점 | 용도 |
|--------|------|------|
| [onSelectFile](/docs/events/on-select-file) | 파일 선택 시 | 파일 이름 확인, 로딩 이미지 표시 |
| [onReceiveData](/docs/events/on-receive-data) | 서버 또는 내부 데이터 수신 직후 | 데이터 확인/가공 |
| [onImportFinish](/docs/events/on-import-finish) | 데이터 로드 전 (onBeforeDataLoad과 같은 시점) | 업로드 데이터 검증, 오류 시 로딩 이미지 닫기 |
| [onDataLoad](/docs/events/on-data-load) | 데이터 파싱 완료 | row 객체 접근 |
| [onSearchFinish](/docs/events/on-search-finish) | 렌더링 완료 | 정상 로딩 시 로딩 이미지 닫기 |

### Read More
- [loadExcel method](/docs/funcs/excel/load-excel)
- [importData method](/docs/funcs/core/import-data)
- [loadText method](/docs/funcs/excel/load-text)
