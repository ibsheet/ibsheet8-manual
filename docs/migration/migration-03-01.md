# 이벤트 사용 방법 변경

IBSheet7에서 이벤트는 global window객체 안에 `시트id_이벤트명` 형식의 함수를 만드는 형태였습니다.<br/>
IBSheet8에서는 다른 속성과 마찬가지로 [Events](/docs/start/basic-structure)라는 속성명안에서 필요한 이벤트를 정의하는 형태로 변경되었습니다.<br/>
또한 각 이벤트별로 달랐던 argument의 개수도 IBSheet8에서는 모든 이벤트가 동일하게 `evtParam` 객체 하나를 받고, `evtParam` 객체안에 각 이벤트에 따라 다른 인자를 갖는 형태로 바뀌었습니다.
```javascript
//AS-IS
//change 이벤트
function mySheet_OnChange(row, col, value, oldValue) {
    if (col == 5 && value > 100) {
        alert("최대 100 까지 입력 가능합니다.");
    }
}
//click 이벤트
function mySheet_OnClick(row, col, value, cellx, celly, cellw, cellh, rowtype) {
    if (mySheet.ColSaveName(col) == "SA_NO") {
        showEmpPopup( value ,"simple" );
    }
}
```
```javascript
//TO-BE
opt.Events = {
    //change 이벤트
    onAfterChange:function(evtParam) {
        if (evtParam.col == "AVGRST" && evtParam.val > 100 ) {
            alert("최대 100 까지 입력 가능합니다.");
        }
    },
    //click 이벤트
    onAfterClick:function(evtParam) {
        if (evtParam.col == "SA_NO") {
            showEmpPopup( evtParam.sheet.getValue(evtParam.row, evtParam.col) );
        }
    }
}
```
