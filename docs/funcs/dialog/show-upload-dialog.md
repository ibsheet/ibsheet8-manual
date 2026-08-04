# showUploadDialog ***(method)***
> 엑셀 업로드 시 옵션을 선택할 수 있는 다이얼로그입니다.  
> 엑셀뿐만 아니라 `txt`, `csv` 파일도 업로드할 수 있습니다.  
> 해당 함수는 `/plugins/ibsheet-dialog.js` 파일이 포함되어 있어야 사용하실 수 있습니다.  
> 이 함수는 내부적으로 `loadExcel`을 호출하므로 [AutoExcelMode](/docs/props/cfg/auto-excel-mode) 값에 따라 필요 조건이 달라집니다.  
> - 기본(서버 모듈, `AutoExcelMode:1`): `/plugins/ibsheet-excel.js` 로드와 `Cfg.Export.Url`(`jsp`/`aspx`) 설정이 필요합니다.  
> - 클라이언트 모듈(`AutoExcelMode:2`): 내부적으로 `importData`로 처리되어 브라우저에서 업로드하므로 `ibsheet-excel.js`/`Export.Url`이 필요 없습니다.  
> 다이얼로그 커스터마이징은 [Dialog Templates appendix](/docs/appx/dialog-templates)를 참고하세요.

###
![업로드 다이얼로그](/assets/imgs/showuploaddialog_recent.png)

### 상세 설명
> 업로드 다이얼로그의 **맨 윗줄(헤더 행)** 에는 컬럼마다 매핑 선택 항목이 있습니다. 
> 여기서 엑셀에서 올라온 각 컬럼을 대상 시트의 어느 컬럼에 넣을지 지정하며, 선택지에는 대상 시트의 헤더가 표시됩니다(필수 컬럼은 이름 옆에 `(필수)`). 
> 선택한 컬럼으로 데이터가 반영됩니다. 이때 매핑한 컬럼의 형식(숫자, 날짜, `Enum` 등)이나 필수 조건에 맞지 않는 값은 노란색으로 표시되며, 
> 해당 셀을 조건에 맞게 수정해야 업로드할 수 있습니다. (예: 숫자 컬럼에 매핑했는데 값이 문자면 노란색으로 표시되고, 숫자로 수정해야 로드됩니다.)  

![헤더 매핑](/assets/imgs/showuploaddialog_mapping.png "헤더 매핑 - 업로드 컬럼을 대상 시트 컬럼에 매핑")  

> 매핑 방식은 `headType`으로 지정합니다. (`"select"`: 드롭다운 / `"drag"`: 드래그&드롭)  
> 팝업의 앞쪽 체크박스로 일부 행을 로드에서 제외할 수 있으며, 로드된 데이터는 일부 수정할 수 있습니다.  
> `colCount` 기본값은 `20`이며, 과도하게 설정하면 성능에 영향을 줄 수 있습니다. `txt`는 열 구분자를 직접 선택할 수 있습니다.

### Syntax
```javascript
void showUploadDialog( uploadType, width, height, name, colCount, fullLoad, headType );
```

### Parameters
|Name|Type|Required| Description |
|----------|-----|---|----|
|uploadType|`string`|<span class='required'>필수</span>|업로드할 파일 형식 (`'excel'`, `'txt'`, `'csv'`)|
|width|`number`|<span class='optional'>선택</span>|다이얼로그 가로 크기 (`default: 700`)|
|height|`number`|<span class='optional'>선택</span>|다이얼로그 세로 크기 (`default: 400`)|
|name|`string`|<span class='optional'>선택</span>|다이얼로그 시트 이름 (`default: "excelUploadSheet_" + 시트id`)|
|colCount|`number`|<span class='optional'>선택</span>|실제 엑셀 파일의 컬럼 수가 더 많을 수 있어, 여분의 임의 컬럼을 미리 만들어 둡니다 (`default: 20`)|
|fullLoad|`boolean`|<span class='optional'>선택</span>|loadExcel({mode:"FullLoad"})와 동일한 업로드 다이얼로그 사용 여부 (`default: false`)|
|headType|`string`|<span class='optional'>선택</span>|헤더 매핑 방식 지정 <br/>(`"select"`: select box 방식 / `"drag"`: drag&drop 방식)<br/>(`default: "select"`)|


### Return Value
***none***

### Example
```javascript
//excel 업로드 다이얼로그 생성
sheet.showUploadDialog("excel");

//txt 업로드 다이얼로그 생성
sheet.showUploadDialog("txt");

//객체 형식
sheet.showUploadDialog({
  uploadType:"excel",
  colCount: 25
});
```
### Read More
- [Dialog Templates appendix](/docs/appx/dialog-templates)
- [showDialog static](/docs/static/show-dialog)
- [Dialog appendix](/docs/appx/dialog)
- [loadExcel method](/docs/funcs/excel/load-excel)
- [loadText method](/docs/funcs/excel/load-text)
- [showDownloadDialog method](./show-download-dialog)

### Since

|product|version|desc|
|---|---|---|
|dialog|0.0.2|기능 추가 및 업로드할 시트가 `Cfg.MultiRecord` 기능을 사용할때 대응 할 수 있도록 수정|
|dialog|1.0.46|fullLoad, headType 인자 추가<br/>HTML/CSS를 dlgTemplates 외부 템플릿 파일로 분리|
