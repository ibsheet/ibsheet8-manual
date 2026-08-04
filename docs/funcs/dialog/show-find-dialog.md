# showFindDialog ***(method)***

> 시트 내에 데이터(텍스트 기준)를 찾기 위한 다이얼로그를 오픈합니다.  
> 바꾸기 기능을 통해 검색 데이터를 변경할 수 있습니다.  
> 해당 함수는 `"/plugins/ibsheet-dialog.js"` 파일이 포함되어 있어야 사용하실 수 있습니다.  
> 다이얼로그 커스터마이징은 [Dialog Templates appendix](/docs/appx/dialog-templates)를 참고하세요.

###

**검색 기능** <br/>
![찾기다이얼로그](/assets/imgs/findDialog_search.png) <br/>

**바꾸기 기능** <br/>
![찾기다이얼로그](/assets/imgs/findDialog_replace.png) <br/>

**모두 찾기 기능** <br/>
![찾기다이얼로그](/assets/imgs/findDialog_searchAll.png) <br/>

### Syntax
```javascript
object showFindDialog();
```

### Return Value
***none***

### Example
```javascript
//모든 시트에서 ctrl+shift+F 입력시 찾기창 오픈
IBSheet.CommonOptions = {
  Events:{
    "onKeyDown":function(evtParam){
      //Ctrl+Shift+F 입력시 찾기 창 오픈
      if(evtParam.prefix == "ShiftCtrl" && evtParam.key == 70 ){
        evtParam.sheet.showFindDialog();
      }
    }
  }
};
```

### Read More
- [Dialog Templates appendix](/docs/appx/dialog-templates)
- [showDialog static](/docs/static/show-dialog)
- [Dialog appendix](/docs/appx/dialog)

### Since

|product|version|desc|
|---|---|---|
|dialog|0.0.0|기능 추가|
|dialog|0.0.9|찾기 다이얼로그 리뉴얼 (바꾸기 기능, 전체 셀 내용 일치, 컬럼 선택 기능 추가)|
|dialog|1.0.12|찾기 다이얼로그 리뉴얼 (모두찾기 기능 추가 및 UI 리뉴얼)|
|dialog|1.0.46|HTML/CSS를 dlgTemplates 외부 템플릿 파일로 분리|
|dialog|1.0.79|ctrl+f 단축키로 다이얼로그 뜨도록 기능 개선|
