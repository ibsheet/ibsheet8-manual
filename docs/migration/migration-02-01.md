# 객체 생성

IBSheet7의 객체 생성 단계는 다음과 같습니다.
1. `createIBSheet`(혹은 `createIBSheet2`)함수를 이용하여 기본 시트 객체 생성
2. `SetConfig`(환경 설정), `InitHeaders`(헤더 설정), `InitColumns`(열 설정) 세 함수를 호출하여 시트를 초기화. `IBS_InitSheet`(`ibsheetinfo.js`에서 제공) 함수를 이용했을 때는 내부에서 이 세 함수를 한 번에 호출합니다.

IBSheet8은 위 두개 과정이 합쳐진 형태로 단일 함수내에서 객체에 대한 생성 및 초기화가 이루어지게 됩니다.

> **생성 시점 주의 (동기/비동기)**: IBSheet7은 시트 생성이 무조건 동기 방식이라 생성 함수 호출 직후 곧바로 시트 객체를 사용할 수 있었습니다.  
> IBSheet8의 [create (static)](/docs/static/create)는 기본이 비동기 방식이므로, 함수가 반환한 직후에는 시트가 아직 완성되지 않았을 수 있습니다.  
> 생성 완료 후 데이터 로드나 시트 조작은 [onRenderFirstFinish (event)](/docs/events/on-render-first-finish)에서 처리하는 것을 권장합니다.  
> 반드시 동기로 생성해야 한다면 `create`의 `sync` 인자를 `1`로 지정합니다.

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
