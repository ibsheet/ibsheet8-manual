# 객체 생성(객체 생성 및 초기화)

## 2. 객체 생성 및 초기화 <a name="chapter-2"></a>

### 객체 생성 <a name="create-ibsheet"></a>
IBSheet7의 객체 생성 단계는 다음과 같습니다.
1. `createIBSheet`(혹은 `createIBSheet2`)함수를 이용하여 기본 시트 객체 생성
2. 초기화 함수(`IBS_InitSheet`)를 통해 열의 개수,기능을 설정

IBSheet8은 위 두개 과정이 합쳐진 형태로 단일 함수내에서 객체에 대한 생성 및 초기화가 이루어지게 됩니다.

```javascript
//AS-IS

// 1. 시트 객체를 #sheetDIV 객체에 지정한 크기로 생성(생성객체,id,너비,높이)
createIBSheet2( document.getElementById("sheetDIV"),"mySheet","100%","250px");
// 2. 시트 초기화
var initSheet = {
    Cfg:{SearchMode:2},
    Cols:[
        {Header:"No",Type:"Seq",SaveName:"SEQ",Width:60},
        {Header:"이름",Type:"Text",SaveName:"sName",Width:100,Align:"Center"},
        {Header:"부서",Type:"Combo",SaveName:"sDept",Width:80,ComboText:"인사|총무|개발|설계",ComboCode:"A01|A04|B01|B02"},
        ...
    ]
}
//초기화 함수 호출(시트객체,초기화 설정 구문)
IBS_InitSheet(mySheet,initSheet);
```
```javascript
//TO-BE
var initSheet = {
    Cfg:{SearchMode:2},
    Cols:[
        {Header:"No",Type:"Int",Name:"SEQ",Width:60},
        {Header:"이름",Type:"Text",Name:"sName",Width:100,Align:"Center"},
        {Header:"부서",Type:"Enum",Name:"sDept",Width:80,Enum:"|인사|총무|개발|설계",EnumKeys:"|A01|A04|B01|B02"},
        ...
    ]
}
//시트 객체 생성 및 초기화(높이,너비는 sheetDIV객체의 크기를 따른다)
IBSheet.create({
    el:"sheetDIV" //생성객체
    id:"mySheet" //id
    options:initSheet //초기화 설정 구문

});
```
