# 엑셀 다운로드 이벤트 발생 순서 ***(event flow)***

<!-- synonyms: 엑셀 다운, 엑셀 내보내기, excel download, export -->

> 다운로드 함수([down2Excel](/docs/funcs/excel/down-to-excel), [exportData](/docs/funcs/core/export-data), [down2Text](/docs/funcs/excel/down-to-text), [down2Pdf](/docs/funcs/excel/down-to-pdf)) 호출 시 이벤트 발생 순서입니다.

### 발생 순서

[onBeforeExport](/docs/events/on-before-export) → 파일 다운로드 → [onExportFinish](/docs/events/on-export-finish)

### 이벤트별 시점 및 용도

| 이벤트 | 시점 | 용도 |
|--------|------|------|
| [onBeforeExport](/docs/events/on-before-export) | 다운로드 시작 전 | 다운로드 취소 (return true), 데이터 검증, 로딩 이미지 표시 |
| [onExportFinish](/docs/events/on-export-finish) | 파일 다운로드 완료 후 | 로딩 이미지 닫기 |

### Read More
- [down2Excel method](/docs/funcs/excel/down-to-excel)
- [exportData method](/docs/funcs/core/export-data)
- [down2Text method](/docs/funcs/excel/down-to-text)
- [down2Pdf method](/docs/funcs/excel/down-to-pdf)
- [directDown2Excel method](/docs/funcs/excel/direct-down-to-excel)
