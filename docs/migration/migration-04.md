# 자주 사용되는 함수 대응

## 4. 자주 사용되는 함수 대응 <a name="chapter-4"></a>

IBSheet7에서 비교적 자주 사용되었다고 생각되는 함수에 대해 지원 여부와 변경된 내용입니다.

|IBSheet7 함수명|기능 설명|IBSheet8 지원 여부|
|---|---|---|
|ActionMenu|데이터 영역에서 마우스 우측 버튼 클릭시 컨텍스트 메뉴 생성|[Menu](/docs/appx/menu)속성으로 대체|
|CellAlign|셀의 좌우 정렬 값 설정|[Align (cell)](/docs/props/cell/align)속성으로 대체.<br/>ex) `sheet.setAttribute(row,'colName','Align','Right');`|
|CellBackColor|셀의 배경색 변경|[Color (cell)](/docs/props/cell/color)속성으로 대체.<br/>ex) `var color = sheet.getAttribute(row, 'colName', 'Color');`|
|CellComboItem|셀의 드롭리스트 아이템 변경|[Enum (cell)](/docs/props/cell/enum), [EnumKeys (cell)](/docs/props/cell/enum-keys) 속성으로 대체.<br/>ex) `sheet.setAttribute(row, 'colName', 'Enum', '\|사장\|과장\|대리\|사원');`<br/>`sheet.setAttribute(row, 'colName', 'EnumKeys', '\|A01\|B0\|B2\|C0');`|
|CellEditable|셀의 편집가능 여부|[CanEdit (cell)](/docs/props/cell/can-edit)속성으로 대체.<br/>ex) `sheet.setAttribute(row, 'colName', 'CanEdit', 0);`|
|CellFont|셀의 다양한 폰트 유형 설정|[TextFont (cell)](/docs/props/cell/text-font), [TextStyle (cell)](/docs/props/cell/text-style), [TextSize (cell)](/docs/props/cell/text-size) 속성으로 대체<br/>ex) `sheet.setAttribute(row, 'colName', 'TextSize', '1.3em');`|
|CellFontBold|셀의 font-weight 수정|[TextStyle (cell)](/docs/props/cell/text-style)속성으로 대체<br/>ex) `sheet.setAttribute(row, 'colName', 'TextStyle', 1);`|
|CellFontColor|셀의 폰트 색상 변경|[TextColor (cell)](/docs/props/cell/text-color)속성으로 대체<br/>ex) `var color = sheet.getAttribute(row, 'colName', 'TextColor');`|
|CellFontItalic|셀의 font-style를 italic으로 수정|[TextStyle (cell)](/docs/props/cell/text-style)속성으로 대체<br/>ex) `sheet.setAttribute(row, 'colName', 'TextStyle', 2);`|
|CellFontName|셀의 font-family 수정|[TextFont (cell)](/docs/props/cell/text-font)속성으로 대체<br/>ex) `sheet.setAttribute(row, 'colName', 'TextFont', '맑은 고딕');`|
|CellFontSize|셀의 font-size 수정|[TextSize (cell)](/docs/props/cell/text-size)속성으로 대체<br/>ex) `sheet.setAttribute(row, 'colName', 'TextSize', '1.5em');`|
|CellFontStrike|셀 내용에 취소선(strike) 설정|[TextStyle (cell)](/docs/props/cell/text-style)속성으로 대체<br/>ex) `sheet.setAttribute(row, 'colName', 'TextStyle', 8);`|
|CellFontUnderline|셀 내용에 밑줄(Underline) 설정|[TextStyle (cell)](/docs/props/cell/text-style)속성으로 대체<br/>ex) `sheet.setAttribute(row, 'colName', 'TextStyle', 4);`|
|CellVAlign|셀 내용의 상하 정렬 설정|[VAlign (cell)](/docs/props/cell/v-align)속성으로 대체<br/>ex) `sheet.setAttribute(row, 'colName', 'VAlign', 'top');`|
|CellImage|이미지 셀의 이미지 변경|[getValue (method)](/docs/funcs/core/get-value), [setValue (method)](/docs/funcs/core/set-value)함수로 변경([Img타입에 대한 데이터 확인](/docs/appx/type))<br/>ex) `sheet.setValue(row, 'colName', '\|./img/pic/sw97231.png\|200\|300');`|
|CellSearchValue|셀의 최초 로딩된 데이터 확인|[Orig (cell)](/docs/props/cell/orig)속성으로 대체<br/>ex) `var orgValue = sheet.getAttribute( sheet.getRowById("AR99") , "CLS" , "Orig");`|
|CellText|셀의 값을 포맷이 적용된 상태로 얻거나 설정|[getString (method)](/docs/funcs/core/get-string), [setString (method)](/docs/funcs/core/set-string)함수로 대체<br/>ex) `var v = sheet.getString(row, col);`|
|CellValue|셀의 값을 포맷을 제거한 상태로 얻거나 설정|[getValue (method)](/docs/funcs/core/get-value), [setValue (method)](/docs/funcs/core/set-value)함수로 대체<br/>ex) `sheet.setValue(row, 'colName', 'A01');`|
|CheckAll|열 전체에 값을 체크|[setAllCheck (method)](/docs/funcs/core/set-all-check)함수로 대체<br/>ex) `sheet.setAllCheck('colName', 1);` |
|CheckedRows|체크된 전체 행의 개수를 얻음|[getRowsByChecked (method)](/docs/funcs/core/get-rows-by-checked)함수를 이용<br/>ex)  `var cnt = sheet.getRowsByChecked( 'sCheck' ).length;`|
|ColBackColor|열 전체의 배경색 설정|[Color (col)](/docs/props/col/color)속성으로 대체<br/>ex) `sheet.setAttribute(null, 'colName', 'Color', '#FF9AE0');`|
|ColFontBold|열 전체의 font-weight를 설정|[TextStyle (col)](/docs/props/col/text-style)속성으로 대체<br/>ex) `sheet.setAttribute(null, 'colName', 'TextStyle', 1);`|
|ColFontColor|열 전체의 글자색을 설정|[TextColor (col)](/docs/props/col/text-color)속성으로 대체<br/>ex) `sheet.setAttribute(null, 'colName', 'TextColor', '#FF0000');`|
|ColFontUnderline|열 전체 내용에 밑줄(Underline)설정|[TextStyle (col)](/docs/props/col/text-style)속성으로 대체<br/>ex) `sheet.setAttribute(null, 'colName', 'TextStyle', 4);`|
|ColWidth|열의 너비 설정|[Width (col)](/docs/props/col/width)속성으로 대체<br/>ex) `sheet.setAttribute(null, 'colName', 'Width', 250);`|
|ColEditable|열의 편집 가능여부 설정|[CanEdit (col)](/docs/props/col/can-edit)속성으로 대체<br/>ex) `sheet.setAttribute(null, 'colName', 'CanEdit', 0);`|
|ColInsert|신규 열 추가 기능|[addCol (method)](/docs/funcs/core/add-col)함수로 변경|
|ColHidden|열 보임/감춤 설정|[showCol (method)](/docs/funcs/core/show-col), [hideCol (method)](/docs/funcs/core/hide-col)함수로 변경|
|ColSaveName|열 index를 기준으로 `Name`을 확인|[getColByIndex (method)](/docs/funcs/core/get-col-by-index)함수로 대체<br/>ex) `var c = sheet.getColByIndex(4);`|
|ColumnSort|지정한 열 소팅|[doSort (method)](/docs/funcs/core/do-sort)함수로 대체<br/>ex) `sheet.doSort('colName1|-colName2');`|
|ColValueDup|열내 중복행 검사|[getRowsByDup (method)](/docs/funcs/core/get-rows-by-dup)함수로 대체<br/>ex) `var dupRows = sheet.getRowsByDup({cols:'colName','firstOnly':1});`|
|ColValueDupRows|열내 전체 중복행 추출|[getRowsByDup (method)](/docs/funcs/core/get-rows-by-dup)함수로 대체<br/>ex) `var dupRows = sheet.getRowsByDup({cols:'colName'});`|
|CountFormat|조회건수 표시|[setInfoRow (method)](/docs/funcs/core/set-info-row)함수로 대체|
|CountPosition|조회 건수 표시 위치|[setInfoRow (method)](/docs/funcs/core/set-info-row)함수로 대체|
|CurrentColInfo|현재 열 정보(순서,너비등) 추출|[getCurrentInfo (method)](/docs/funcs/core/get-current-info), [setCurrentInfo (method)](/docs/funcs/core/set-current-info)함수로 변경|
|DataCopy|행 복사 기능|[copyRow (method)](/docs/funcs/core/copy-row)함수로 대체<br/>ex) `sheet.copyRow(sheet.getFocusedRow());`|
|DataInsert|행 추가 기능|[addRow (method)](/docs/funcs/core/add-row)함수로 대체<br/>ex) `sheet.addRow();`|
|DataMove|행 이동 기능|[moveRow (method)](/docs/funcs/core/move-row)함수로 대체<br/>ex) `sheet.moveRow(row, nextRow);`|
|DirectDown2Excel|시트의 조회 데이터 대신 서버에서 직접 만든 데이터로 엑셀 다운로드|[directDown2Excel (method)](/docs/funcs/excel/direct-down-to-excel)함수로 동일|
|DirectLoadExcel|사용자가 선택한 엑셀 파일을 시트에 로드하지 않고 지정한 서버로 바로 전달|[directLoadExcel (method)](/docs/funcs/excel/direct-load-excel)함수로 동일|
|DoAllSave|전체 데이터 저장|[doSave (method)](/docs/funcs/core/do-save)함수에 `saveMode`인자로 대체<br/>ex) `sheet.doSave({url:'saveData.do',saveMode:0});`|
|DoPrint|시트데이터 인쇄|[doPrint (method)](/docs/funcs/core/do-print)함수로 동일|
|DoSave|시트 데이터 저장|[doSave (method)](/docs/funcs/core/do-save)함수로 동일|
|DoSearch|시트 데이터 조회|[doSearch (method)](/docs/funcs/core/do-search)함수로 동일|
|DoSearchPaging|SearchMode가 서버페이징 인 경우 조회 함수|[doSearchPaging (method)](/docs/funcs/core/do-search-paging)함수로 동일|
|Down2Excel|시트를 excel파일로 export|[down2Excel (method)](/docs/funcs/excel/down-to-excel)함수로 동일 (엑셀 모듈 방식)<br/>클라이언트(jszip) 방식으로 내려받으려면 [exportData (method)](/docs/funcs/core/export-data) 사용|
|Down2ExcelBuffer|여러개의 시트를 엑셀파일로 export|[down2ExcelBuffer (method)](/docs/funcs/excel/down-to-excel-buffer)함수로 동일 (엑셀 모듈 방식)<br/>클라이언트(jszip) 방식으로 내려받으려면 [exportDataBuffer (method)](/docs/funcs/core/export-data-buffer) 사용|
|Down2Pdf|시트의 내용을 PDF 파일로 다운로드|[down2Pdf (method)](/docs/funcs/excel/down-to-pdf)함수로 동일|
|Down2Text|시트의 내용을 text파일로 export|[down2Text (method)](/docs/funcs/excel/down-to-text)함수로 동일 (엑셀 모듈 방식)<br/>클라이언트(jszip) 방식으로 내려받으려면 [exportData (method)](/docs/funcs/core/export-data) 사용 (txt/csv 지원)|
|Editable|시트 전체에 대한 편집가능 여부설정|[CanEdit (cfg)](/docs/props/cfg/can-edit)속성으로 대체|
|EditTabBehavior|편집 상태에서 `Tab` 키 입력 시 동작 설정|[EditTabMode (cfg)](/docs/props/cfg/focus-mode)속성으로 대체|
|EnterBehavior|`Enter` 키 입력 시 동작 설정|[EnterMode (cfg)](/docs/props/cfg/enter-mode)속성으로 대체|
|Enable|시트 활성화 여부|[enable (method)](/docs/funcs/core/enable),[disable (method)](/docs/funcs/core/disable) 두개 함수로 변경|
|ExportData|시트의 데이터를 인자의 형식(json/csv)으로 추출|[getSheetData (method)](/docs/funcs/excel/get-sheet-data)함수로 대체<br/>(이름이 유사한 IBSheet8 `exportData`는 엑셀 파일 다운로드용으로 별개 함수)<br/>ex) `var data = sheet.getSheetData({type: "json"});`|
|ExtendLastCol|마지막 열의 자동 너비 조절 기능|[RelWidth (col)](/docs/props/col/rel-width)속성을 통해 열간 너비 비율 조정 가능|
|FindCheckedRow|특정 열에 체크된 행 추출 기능|[getRowsByChecked (method)](/docs/funcs/core/get-rows-by-checked)함수로 변경|
|FindStatusRow|상태변화된 행 추출 기능|[getRowsByStatus (method)](/docs/funcs/core/get-rows-by-status)함수로 변경 |
|FindSubSumRow|소계/누계 행 추출|[getSubTotalRows (method)](/docs/funcs/core/get-sub-total-rows)함수로 대체<br/>ex) `var subRows = sheet.getSubTotalRows();`|
|FindText|특정 문자를 포함하는 행 추출 기능|[findText (method)](/docs/funcs/core/find-text)함수로 동일|
|FitColWidth|열의 너비 재조정|[RelWidth (col)](/docs/props/col/rel-width)속성을 통해 자동 조정되는 형태로 변경|
|FitSizeCol|열의 너비를 열내에 가장 긴글자를 갖는 셀에 맞게 조정|[fitSize (method)](/docs/funcs/core/fit-size)함수로 변경|
|FocusAfterProcess|데이터 로딩 후 첫번째 행에 포커스를 둘지 여부|[IgnoreFocused (cfg)](/docs/props/cfg/ignore-focused)속성으로 대체<br/>0으로 설정하면 데이터 로딩 후 첫번째 행에 포커스를 이동 시킴 (default: 0)|
|FrozenCol|좌측 열 고정 기능|[setFixedLeft (method)](/docs/funcs/core/set-fixed-left)함수로 변경|
|FrozenRows|상단에 행 고정 기능|[setFixedTop (method)](/docs/funcs/core/set-fixed-top)함수로 변경 |
|GetCellProperty|행또는 셀에 속성 확인 기능|[getAttribute (method)](/docs/funcs/core/get-attribute)함수 통해 확인 가능<br/>ex) `var colEdit = sheet.getAttribute({col:'colName',attr:'CanEdit'});` |
|GetChildRows|트리사용시 특정행의 자식행 추출|[getChildRows (method)](/docs/funcs/core/get-child-rows)함수로 동일|
|GetComboInfo|드랍리스트의 item 내용 확인|[Enum (col)](/docs/props/col/enum), [EnumKeys (col)](/docs/props/col/enum-keys)속성을 통해 확인 가능<br/>ex) `var enum = sheet.getAttribute(null, 'colName', 'Enum');`|
|GetCurrentPage|현재 페이지 index를 확인|[getPageIndex (method)](/docs/funcs/core/get-page-index)함수로 변경|
|GetDataFirstRow|첫번째 데이터행 index 확인|[getFirstRow (method)](/docs/funcs/core/get-first-row)함수로 변경|
|GetDataLastRow|마지막 데이터행 index 확인|[getLastRow (method)](/docs/funcs/core/get-last-row)함수로 변경|
|GetEditText|현재 편집중인 내용 확인|[getEditText (method)](/docs/funcs/core/get-edit-text)함수로 대체<br/>ex) `var txt = sheet.getEditText();`|
|GetEtcData|조회 응답의 `etc` 추가 데이터 확인|조회 응답을 `{data:[...], etc:{...}}` 형태로 구성하면 `sheet.etc` 속성으로 접근할 수 있습니다.<br/>ex) `var etcData = sheet.etc;`|
|GetSaveData|ajax 통신 전용 함수|[ajax (method)](/docs/funcs/core/ajax)함수로 대체|
|GetSaveJson|시트 내 데이터를 json형식으로 추출|[getSaveJson (method)](/docs/funcs/core/get-save-json)함수로 동일|
|GetSaveString|시트 내 데이터를 querystring형식으로 추출|[getSaveString (method)](/docs/funcs/core/get-save-string)함수로 동일|
|GetSearchData|ajax 통신 전용 함수|[ajax (method)](/docs/funcs/core/ajax)함수로 대체|
|GetSelectionCols|현재 선택된 열 index 추출|[getSelectedRanges (method)](/docs/funcs/core/get-selected-range)함수를 통해 선택 영역 전체를 얻는 형태로 변경|
|GetSelectionRows|현재 선택된 행 index 추출|[getSelectedRanges (method)](/docs/funcs/core/get-selected-range)함수를 통해 선택 영역 전체를 얻는 형태로 변경|
|HeaderActionMenu|헤더행에서 마우스 우측버튼 클릭시 컨텍스트 메뉴 표시 기능|IBSheet8은 헤더 컨텍스트 메뉴를 기본 제공하며, [UseHeaderContextMenu (cfg)](/docs/props/cfg/use-header-context-menu)로 표시 여부를 제어합니다. (기본값 `1`은 표시, 구현은 `ibsheet-common.js`에 포함)<br/>메뉴 항목을 직접 구성하려면 [Menu (row)](/docs/props/row/menu)속성을 [Def.Header](/docs/appx/init-structure)에 설정합니다.|
|HeaderBackColor|헤더행에 대한 배경색|가급적 css 파일에서 설정하는 것을 권장.<br/>[Def.Header](/docs/appx/init-structure)에 [Color (row)](/docs/props/row/color)속성을 통해 설정 가능<br/>ex) `sheet.setAttribute(sheet.getRowById("Header"), null, 'Color', '#EDEDED');`|
|HeaderCheck|헤더 체크박스에 대한 체크/체크해제 설정|[Checked (cell)](/docs/props/cell/checked)속성을 통해 설정<br/>ex) `sheet.getAttribute(sheet.Header,"CheckData","Checked");`|
|HeaderFontBold|헤더 타이틀 font-weight 설정|가급적 css 파일에서 설정하는 것을 권장.<br/>[Def.Header](/docs/appx/init-structure)에 [TextStyle (row)](/docs/props/row/text-style)속성을 통해 설정 가능<br/>ex) `sheet.setAttribute(sheet.getRowById("Header"), null, 'TextStyle', 1);`|
|HeaderFontColor|헤더 타이틀 글자색 설정|가급적 css 파일에서 설정하는 것을 권장.<br/>[Def.Header](/docs/appx/init-structure)에 [TextColor (row)](/docs/props/row/text-color)속성을 통해 설정 가능<br/>ex) `sheet.setAttribute(sheet.getRowById("Header"), null, 'TextColor', '#FF0000');`|
|HeaderRows|헤더 행의 개수|[getHeaderRows (method)](/docs/funcs/core/get-header-rows)함수로 확인 가능<br/>ex) `var hcnt = sheet.getHeaderRows().length;`|
|HideFilterRow|필터행 제거 기능|[hideFilterRow (method)](/docs/funcs/core/hide-filter-row)함수로 동일|
|HideProcessDlg|대기 이미지 제거|[hideMessage (method)](/docs/funcs/core/hide-message)함수로 변경|
|HideSubSum|소계 행 제거|[removeSubTotal (method)](/docs/funcs/core/remove-sub-total)함수로 변경|
|IBCloseCalendar|달력 제거|[IBSheet.showCalendar (static)](/docs/static/show-calendar)함수로 생성된 객체의 [`다이얼로그객체.Close` (appendix)](/docs/appx/dialog)함수로 변경|
|IBShowCalendar|시트 외부영역에서 달력 오픈|[IBSheet.showCalendar (static)](/docs/static/show-calendar)함수로 변경|
|ImageList|이미지 파일 index 설정|지원안함|
|InitCellProperty|셀단위 설정 변경|각 셀(cell)에서 사용 가능한 속성을 [setAttribute (method)](/docs/funcs/core/set-attribute)로 변경<br/>ex) `sheet.setAttribute(row, 'colName', 'CanEdit', 0);`|
|InitColumns|열 초기화|[IBSheet.create (static)](/docs/static/create)의 `options`(`Cols`/`LeftCols`/`RightCols`)를 통해 열을 설정|
|InitComboNoMatchText|Combo/Enum에서 매칭되지 않는 값일 때 표시할 대체 텍스트|[EnumNoMatchText (col)](/docs/props/col/enum-no-match-text)속성으로 대체 (`EnumStrictMode:1`과 함께 사용)|
|InitHeaders|헤더 기본 기능 설정|헤더 타이틀은 [Header (col)](/docs/props/col/header)로 설정하고, 소팅, 리사이징, 열이동 등 헤더 기능은 [Cfg](/docs/appx/init-structure)의 [CanSort (cfg)](/docs/props/cfg/can-sort), [CanColResize (cfg)](/docs/props/cfg/can-col-resize), [CanColMove (cfg)](/docs/props/cfg/can-col-move) 등으로 설정.<br/>ex) `options.Cfg = {CanColResize:0, CanColMove:0, CanSort:1}; // 리사이징, 열이동 금지, 소팅 허용`|
|IsDataModified|데이터 수정 여부 확인|[hasChangedData (method)](/docs/funcs/core/has-changed-data)함수로 변경|
|IsHaveChild|자식노드 유무확인|[getChildRows (method)](/docs/funcs/core/get-child-rows)를 이용해서 반환되는 배열의 길이가 0이상이면 자식이 1개 이상 존재하는걸 알 수 있음|
|LastCol|마지막 열 index 얻기|[getLastCol (method)](/docs/funcs/core/get-last-col)함수로 변경(열의 Name이 리턴)|
|LastRow|마지막 행 index 얻기|[getLastRow (method)](/docs/funcs/core/get-last-row)함수로 변경(마지막 데이터 행 객체를 리턴)|
|LoadSaveData|저장 결과에 대한 반영|[applySaveResult (method)](/docs/funcs/core/apply-save-result)함수로 변경|
|LoadSearchData|조회 데이터 로드|[loadSearchData (method)](/docs/funcs/core/load-search-data)함수로 동일(xml 지원 안함)|
|LoadExcel|엑셀파일 데이터 로드|[loadExcel (method)](/docs/funcs/excel/load-excel)함수로 동일|
|LoadExcelBuffer|여러개 워크시트 내용 로딩|[loadExcelBuffer (method)](/docs/funcs/excel/load-excel-buffer)함수로 동일|
|LoadText|텍스트 파일 데이터 로드|[loadText (method)](/docs/funcs/excel/load-text)함수로 동일|
|MergeSheet|데이터 자동 병합 기능|[HeaderMerge (cfg)](/docs/props/cfg/header-merge), [DataMerge (cfg)](/docs/props/cfg/data-merge)속성으로 변경|
|MouseCol|마우스 커서가 위치한 열 index|[getMouseCol (method)](/docs/funcs/core/get-mouse-col)함수로 변경(열의 Name 리턴)|
|MouseHoverMode|데이터위에 마우스 Hover시 표현 설정|[Hover (cfg)](/docs/props/cfg/hover)속성으로 변경<br/>ex) `sheet.Hover = 1; //셀단위`|
|MouseRow|마우스 커서가 위치한 행 index|[getMouseRow (method)](/docs/funcs/core/get-mouse-row)함수로 변경(행 객체 리턴)|
|MouseToolTipText|풍선도움말 표시 설정|[showTip (method)](/docs/funcs/core/show-tip)함수로 변경<br/>ex) `sheet.showTip('<div class="warn">분기 마감 3일 전입니다.</div>');`|
|MoveColumnPos|열 위치 변경|[moveCol (method)](/docs/funcs/core/move-col)함수로 변경|
|PagingPosition|페이지네이션 설정|[InfoRowConfig (cfg)](/docs/props/cfg/info-row-config)속성에 통합|
|RangeBackColor|특정 영역의 배경색 변경|범위 내 셀의 [Color (cell)](/docs/props/cell/color)을 [setRangeAttribute (method)](/docs/funcs/common/set-range-attribute)로 일괄 설정<br/>ex) `sheet.setRangeAttribute(sheet.getRowById("AR1"), "Col1", sheet.getRowById("AR3"), "Col2", "Color", "#FF9AE0");`|
|RangeFontBold|특정 영역의 font-weight 변경|범위 내 셀의 [TextStyle (cell)](/docs/props/cell/text-style)을 [setRangeAttribute (method)](/docs/funcs/common/set-range-attribute)로 일괄 설정<br/>ex) `sheet.setRangeAttribute(sheet.getRowById("AR1"), "Col1", sheet.getRowById("AR3"), "Col2", "TextStyle", 1);`|
|RangeFontColor|특정 영역의 글자색 변경|범위 내 셀의 [TextColor (cell)](/docs/props/cell/text-color)을 [setRangeAttribute (method)](/docs/funcs/common/set-range-attribute)로 일괄 설정<br/>ex) `sheet.setRangeAttribute(sheet.getRowById("AR1"), "Col1", sheet.getRowById("AR3"), "Col2", "TextColor", "#FF0000");`|
|RangeText|특정 영역의 값 설정 (포맷 적용)|범위 내 셀의 값을 [setRangeValue (method)](/docs/funcs/common/set-range-value)로 일괄 설정 (`type:2`이면 [setString (method)](/docs/funcs/core/set-string) 방식으로 포맷 적용)<br/>ex) `sheet.setRangeValue("텍스트", sheet.getRowById("AR1"), "Col1", sheet.getRowById("AR3"), "Col2", null, null, 2);`|
|RangeValue|특정 영역의 값 설정 (포맷 제거)|범위 내 셀의 값을 [setRangeValue (method)](/docs/funcs/common/set-range-value)로 일괄 설정 (`type:1`이면 [setValue (method)](/docs/funcs/core/set-value) 방식)<br/>ex) `sheet.setRangeValue(100, sheet.getRowById("AR1"), "Col1", sheet.getRowById("AR3"), "Col2", null, null, 1);`|
|RedrawSum|합계 재 계산|[calculate (method)](/docs/funcs/core/calculate)함수로 변경|
|RemoveAll|전체 데이터 삭제|[removeAll (method)](/docs/funcs/core/remove-all)함수로 동일|
|RenderSheet|수정 내용 일시 반영 중지/실행|[renderBody (method)](/docs/funcs/core/render-body), [rerender (method)](/docs/funcs/core/rerender)함수로 변경|
|ReNumberSeq|Seq열에 대한 다시 순번 매김|지원안함<br/>매번 자동으로 순번을 계산함.|
|Reset|시트 객체 클리어|[dispose (method)](/docs/funcs/core/dispose)함수를 호출해서 시트를 완전히 제거하고 같은 id로 다시 생성([IBSheet.create (static)](/docs/static/create))|
|ReturnCellData|셀 데이터를 최초 로딩된 데이터로 변경|[revertCell (method)](/docs/funcs/core/revert-cell)함수로 변경|
|ReturnColumnPos|열의 순서를 최초 생성상태로 되돌림|순서만 복원하는 함수는 없음. [revertCol (method)](/docs/funcs/core/revert-col)이 가장 유사하나, 열 순서뿐 아니라 너비, 숨김, 정렬까지 함께 생성 시점으로 복원됨|
|ReturnData|행 전체 데이터를 최초 로딩된 데이터로 변경|[revertRow (method)](/docs/funcs/core/revert-row)함수로 변경|
|RowBackColor|행 배경색 변경|[Color (row)](/docs/props/row/color)속성으로 대체<br/>ex) `sheet.setAttribute(row, null, 'Color', '#FFAA99');`|
|RowBackColorD|삭제될 행의 배경색|css파일 `.IBColorDeleted` class에서 설정|
|RowBackColorI|추가행의 배경색|css파일 `.IBColorAdded` class에서 설정|
|RowBackColorU|수정된 행의 배경색|css파일 `.IBColorChanged` class에서 설정|
|RowCount|상태별 행 개수 확인|[getRowsByStatus (method)](/docs/funcs/core/get-rows-by-status)나 [getTotalRowCount (method)](/docs/funcs/core/get-total-row-count)함수로 확인 가능|
|RowData|행의 값을 json형태로 얻거나 설정|[getRowValue (method)](/docs/funcs/core/get-row-value)로 행 데이터를 json으로 얻고, [setRowValue (method)](/docs/funcs/core/set-row-value)로 json 데이터를 행에 설정<br/>ex) `var data = sheet.getRowValue(sheet.getRowById("AR5"));`<br/>`sheet.setRowValue(sheet.getRowById("AR1"), data);`|
|RowDelete|행 즉시 삭제|[removeRow (method)](/docs/funcs/core/remove-row)함수로 변경|
|RowEditable|행 전체 수정 가능 여부 설정|[CanEdit (row)](/docs/props/row/can-edit)속성으로 대체<br/>ex) `sheet.setAttribute(row, null, 'CanEdit', 0);`|
|RowExpanded|트리 사용시 자식행에 대한 펼침 여부 설정|[setExpandRow (method)](/docs/funcs/core/set-expand-row)함수로 변경|
|RowFontColor|행의 글자색 변경|[TextColor (row)](/docs/props/row/text-color)속성으로 대체<br/>ex) `var fc = sheet.getAttribute(row, null, 'TextColor');`|
|RowHeight|행의 높이 설정|[getRowHeight (method)](/docs/funcs/core/get-row-height)함수로 확인<br/>[Height (row)](/docs/props/row/height)속성으로 높이 변경.<br/>ex) `sheet.setAttribute(sheet.getFocusedRow(), null, "Height", 200);`|
|RowHeightMax|전체 데이터 행의 최대 높이 설정|시트 생성 시 [Def.Row.MaxHeight](/docs/appx/init-structure)속성으로 설정<br/>ex) `options.Def.Row.MaxHeight = 100;`|
|RowHeightMin|전체 데이터 행의 최소 높이를 설정|시트 생성 시 [Def.Row.MinHeight](/docs/appx/init-structure)속성으로 설정<br/>ex) `options.Def.Row.MinHeight = 50;`|
|RowHidden|행을 보임/감춤 설정|[showRow (method)](/docs/funcs/core/show-row), [hideRow (method)](/docs/funcs/core/hide-row)함수로 변경|
|RowLevel|트리 사용시 행의 Depth index 설정|`Level`속성으로 대체(확인만 가능)<br/>ex) `var lvl = sheet.getAttribute(row, null, 'Level');`<br/>[moveRow (method)](/docs/funcs/core/move-row)함수로 행을 이동시켜야함.|
|SaveNameCol|열 명에 대한 Index|[getColIndex (method)](/docs/funcs/core/get-col-index)함수로 변경|
|SearchRows|로드된 데이터 행의 수|[getDataRows (method)](/docs/funcs/core/get-data-rows)함수로 변경<br/>하지만 상태가 변경된 데이터행을 제외하고 싶다면 다음과 같이 개수를 구할 수 있습니다.<br/>ex) `var searchRow = sheet.getDataRows() - sheet.getRowsByStatus("Added,Deleted").length;`|
|SelectCell|특정 위치로 포커스 이동|[focus (method)](/docs/funcs/core/focus)함수로 변경<br/>ex) `sheet.focus(row, 'colName');`|
|SelectCol|특정 열로 포커스 이동|[focus (method)](/docs/funcs/core/focus)함수로 변경<br/>ex) `sheet.focus(null, 'colName');`<br/>`var fc = sheet.getFocusedCol();`|
|SelectionMode|행,셀단위 select 설정|[SelectingCells (cfg)](/docs/props/cfg/selecting-cells)속성으로 대체|
|SelectRow|특정 행으로 포커스 이동|[focus (method)](/docs/funcs/core/focus)함수로 변경<br/>ex) `sheet.focus(row, null);`<br/>`var fr = sheet.getFocusedRow();`|
|SetBlur|시트내 포커스 제거|[blur (method)](/docs/funcs/core/blur)함수로 변경<br/>ex) `sheet.blur(2);`|
|SetColProperty|열 속성 변경|[setAttribute (method)](/docs/funcs/core/set-attribute)를 통해 각종 속성 설정 가능<br/>ex) `sheet.setAttribute(null, 'colName', 'CanEdit', 0);`|
|SetConfig|초기 기능 설정|[IBSheet.create (static)](/docs/static/create)함수에 [Cfg](/docs/appx/init-structure)속성으로 대체|
|SetEndEdit|편집 종료 기능|[endEdit (method)](/docs/funcs/core/end-edit)함수로 변경|
|SetHeaderMode|헤더행에 대한 기능 설정|함수로는 지원안함.<br/>헤더 기능(소팅, 리사이징 등)은 [Cfg](/docs/appx/init-structure)의<br/>[CanSort (cfg)](/docs/props/cfg/can-sort), [CanColResize (cfg)](/docs/props/cfg/can-col-resize) 등 속성으로 설정|
|SetMergeCell|특정 영역에 대한 span|[setMergeRange (method)](/docs/funcs/core/set-merge-range)함수로 변경|
|SetSelectRange|특정 영역 선택|[selectRange (method)](/docs/funcs/core/select-range)함수로 변경|
|SetSplitMergeCell|머지된 영역에 대해 머지취소|[setMergeCancel (method)](/docs/funcs/core/set-merge-cancel)함수로 변경|
|SheetWidth|시트의 너비 변경|[IBSheet.create (static)](/docs/static/create)함수로 생성할때 지정된 el객체의 너비를 수정|
|SheetHeight|시트의 높이 변경|[IBSheet.create (static)](/docs/static/create)함수로 생성할때 지정된 el객체의 높이 수정|
|ShowCalendar|특정 셀 위에 달력 팝업 open|[showCalendar (method)](/docs/funcs/core/show-calendar)함수로 변경<br/>`Date` 타입 열: 함수 호출 시 달력이 표시되고, 날짜 선택 시 셀 값이 자동 입력됨<br/>`Text` 등 그 외 타입: 달력만 표시되고 값은 자동 입력되지 않으므로, 콜백(`func` 인자)에서 [setValue (method)](/docs/funcs/core/set-value)로 직접 넣는 후속 처리 필요<br/>ex) `sheet.showCalendar(row, 'textCol', {Format:'yyyy-MM-dd'}, null, function(ms){ sheet.setValue(row, 'textCol', IBSheet.dateToString(ms, 'yyyy-MM-dd')); });`<br/>(편집 모드 진입 시 자동 표시는 [AutoCalendar (cfg)](/docs/props/cfg/auto-calendar))|
|ShowColumnPopup|열에 설정한 컨텍스트 메뉴를 표시|[showMenu (method)](/docs/funcs/core/show-menu)함수로 유사하게 기능 구현 가능<br/>ex) `var menu = sheet.getAttribute(sheet.getFocusedRow(),"sCompany","Menu");`<br/>`sheet.showMenu(sheet.getFocusedRow(),"sCompany",menu);`|
|ShowFilterRow|필터행 표시|[showFilterRow (method)](/docs/funcs/core/show-filter-row)함수로 동일 |
|ShowFindDialog|찾기 다이얼로그 창 open|[showFindDialog (method)](/docs/funcs/dialog/show-find-dialog)함수로 동일(`ibsheet-dialog.js` 파일 필요)|
|ShowGroupRow|그룹행 생성|[showGroupRow (method)](/docs/funcs/core/show-group-row)함수로 동일<br/>ex) `sheet.showGroupRow("sName");`|
|ShowMsgMode|메시지 표시 여부 설정 및 메시지 가공|[SuppressMessage (cfg)](/docs/props/cfg/suppress-message)속성과 [onShowMessage (event)](/docs/events/on-show-message)로 대체.<br/>IBSheet7은 메시지가 `alert`로 표시되어 `OnMessage` 이벤트에서 직접 `div`로 가공했으나, IBSheet8은 메시지가 기본적으로 `div`로 표시됩니다.<br/>표시할 메시지 종류는 `SuppressMessage`로 조정합니다.<br/>ex) `options.Cfg.SuppressMessage = 2; // 조회/저장 메시지 표시`<br/>메시지를 직접 디자인해 가공하려면 `onShowMessage` 이벤트에서 처리합니다. (IBSheet7의 `OnMessage` 이벤트에 대응)|
|ShowPivotDialog|피봇 다이얼로그 창 open|[showPivotDialog (method)](/docs/funcs/dialog/show-pivot-dialog)함수로 변경(`ibsheet-dialog.js` 파일 필요)|
|ShowProcessDlg|대기 이미지 표시|[showMessage (method)](/docs/funcs/core/show-message)함수로 변경|
|ShowSubSum|소계행 생성 기능|[makeSubTotal (method)](/docs/funcs/core/make-sub-total)함수로 변경|
|ShowToolTip|풍선도움말 표시|[showTip (method)](/docs/funcs/core/show-tip)함수로 변경|
|ShowTreeLevel|트리 시트 사용시 지정한 Depth까지 펼침|[showTreeLevel (method)](/docs/funcs/core/show-tree-level)함수로 동일|
|SubSumBackColor|소계 행의 배경색|[makeSubTotal (method)](/docs/funcs/core/make-sub-total)의 `color` 옵션이나 [Def.SubSum](/docs/appx/init-structure)의 `Color`로 설정 (소계행은 css로 스타일 변경 불가)<br/>ex) `sheet.makeSubTotal([{stdCol:'sName', sumCols:'amt', color:'#dbe2eb'}]);`|
|SumBackColor|합계 행에 대한 배경색|css파일의 `.IBFormulaRow` class에서 설정 혹은 합계행에 대해 직접 설정<br/>ex) `var frow = sheet.getRowById("FormulaRow");`<br/>`sheet.setAttribute(frow, null, 'Color', "#FF0099");`|
|SumFontBold|합계 행에 대한 font-weight|css파일의 `.IBFormulaRow` class에서 설정 혹은 합계행에 대해 직접 설정<br/>ex) `var frow = sheet.getRowById("FormulaRow");`<br/>`sheet.setAttribute(frow, null, 'TextStyle', 1);`|
|SumFontColor|합계 행에 대한 글자색 설정|css파일의 `.IBFormulaRow` class에서 설정 혹은 합계행에 대해 직접 설정<br/>ex) `var frow = sheet.getRowById("FormulaRow");`<br/>`sheet.setAttribute(frow, null, 'TextColor', '#FF0000');`|
|SumRowHidden|합계 행 보입/감춤 설정|[showRow (method)](/docs/funcs/core/show-row), [hideRow (method)](/docs/funcs/core/hide-row)로 분리 및 변경<br/>[Visible (row)](/docs/props/row/visible)속성으로 대체<br/>ex) `var frow = sheet.getRowById("FormulaRow");`<br/>`sheet.setAttribute(frow, null, "Visible", true);`|
|SumValue|합계 행의 값 설정|[getValue (method)](/docs/funcs/core/get-value), [setValue (method)](/docs/funcs/core/set-value)함수로 변경<br/>ex) `var frow = sheet.getRowById("FormulaRow");`<br/>`sheet.setValue(frow, "sAmt", 250000);`|
|TabBehavior|포커스 상태에서 `Tab` 키 입력 시 동작 설정|지원안함|
|Theme|테마 설정|[setTheme (method)](/docs/funcs/core/set-theme)함수로 동일|
|ToolTipText|특정 셀에 풍선도움말 설정|[Tip (cell)](/docs/props/cell/tip)속성으로 대체<br/>ex) `sheet.setAttribute(row, 'colName', 'Tip', '사원번호를 먼저 입력하세요');`|
|TopRow|최상단의 행 index 확인|[getShownRows (method)](/docs/funcs/core/get-shown-rows)함수로 확인 가능<br/>ex) `var trow = sheet.getShownRows()[0];`|
|TotalRows|전체 데이터 건수 설정/확인|[setTotalRowCount (method)](/docs/funcs/core/set-total-row-count)로 설정, [getTotalRowCount (method)](/docs/funcs/core/get-total-row-count)로 확인<br/>ex) `sheet.setTotalRowCount(1250);`<br/>`var cnt = sheet.getTotalRowCount();`|
|Visible|시트 전체 보임/감춤 설정|[IBSheet.create (static)](/docs/static/create)로 생성할때 지정된 el객체에 대해 display나 visibility 변경|
