# showHtmlEditDialog ***(method)***

<!-- synonyms: show html edit dialog, html edit dialog, row html edit, html row form, edit popup html, html detail dialog, HTML 편집 다이얼로그, HTML 행 편집 창, HTML 편집 팝업, HTML 폼 다이얼로그, showHtmlEditDialog 메소드 -->

> 한 행의 내용을 다이얼로그로 열어 보여줍니다.  
> [showEditDialog](/docs/funcs/dialog/show-edit-dialog)와 용도는 같지만, 행 내용을 IBSheet(그리드)가 아닌 순수 HTML 태그로 표현합니다.  
> 해당 함수는 `"/plugins/ibsheet-dialog.js"` 파일이 포함되어 있어야 사용하실 수 있습니다.  
> 다이얼로그 커스터마이징은 [Dialog Templates appendix](/docs/appx/dialog-templates)를 참고하세요.

###
![showHtmlEditDialog](/assets/imgs/showHtmlEditDialog.png)

### Syntax
```javascript
object showHtmlEditDialog( row, width, height, headerIndex, name, excludeHideCol );
```

### Parameters

|Name|Type|Required| Description |
|----------|-----|---|----|
|row|`object`|<span class='required'>필수</span>|다이얼로그로 보여질 [데이터 로우 객체](/docs/appx/row-object)
|width|`number`|<span class='optional'>선택</span>|다이얼로그 창의 너비 (`default: 700`)|
|height|`number`|<span class='optional'>선택</span>|다이얼로그 창의 높이 (`default: 400`)|
|headerIndex|`number`|<span class='optional'>선택</span>|헤더행이 여러 줄인 경우 몇 번째 헤더행을 다이얼로그의 타이틀로 표시할 지 여부<br>(`default: 모든 헤더행의 타이틀을 구분자 "/"로 연결하여 표시`)|
|name|`string`|<span class='optional'>선택</span>|다이얼로그 이름 (`default: "htmlEditSheet_" + 시트id`)|
|excludeHideCol|`boolean`|<span class='optional'>선택</span>|숨겨진 컬럼에 대한 처리 여부<br>`0(false)`:다이알로그 출력 시, 숨겨진 컬럼 포함 (`default`)<br>`1(true)`:다이알로그 출력 시 숨겨진 컬럼 제외|

### Return Value
***none***

### Example
```javascript
// 특정 열의 셀 클릭 시 다이얼로그 오픈
options.Events = {
  onAfterClick:function(evtParam){
    if(evtParam.col == "DetailBtn"){
      evtParam.sheet.showHtmlEditDialog(evtParam.row);
    }
  }
}

// 객체 방식
sheet.showHtmlEditDialog({row: sheet.getFocusedRow(), width: 700, height: 700});
```

### Read More
- [showEditDialog method](/docs/funcs/dialog/show-edit-dialog)
- [Dialog Templates appendix](/docs/appx/dialog-templates)
- [showDialog static](/docs/static/show-dialog)
- [Dialog appendix](/docs/appx/dialog)

### Since

|product|version|desc|
|---|---|---|
|dialog|1.0.4|기능 추가|
|dialog|1.0.46|HTML/CSS를 dlgTemplates 외부 템플릿 파일로 분리|
