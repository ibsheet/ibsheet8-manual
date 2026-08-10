# event 사용법 기초

<!-- synonyms: 이벤트 사용법, 이벤트 설정 방법, Events 옵션, 이벤트 바인딩, addEventListener 시트, event usage, event setup, event binding -->

> 시트의 이벤트는 아래와 같이 두 가지 방법으로 설정할 수 있습니다.

## 1. 객체 생성시점에서 이벤트 설정하기
시트를 초기화하는 `options` 속성 설정 시 `Events` 속성을 통해 다음과 같이 설정합니다.
```javascript
var OPTS = {
    Cfg:{ ... },
    Cols:[ ... ],
    "Events":{
        onAfterChange:function(evtParam){
            ... 이벤트 발생 시 로직 구현 ...
        }
    }
};
IBSheet.create(
    id:"sheet",
    el:"sheet_div",
    options:OPTS
)
```
## 2. 객체 생성 이후 이벤트 설정하기
객체가 생성되고 난 이후에는 `bind` 함수를 통해 이벤트를 설정하실 수 있습니다.
```javascript
    // onAfterChange 이벤트
    sheet.bind("onAfterChange", function(evtParam) {

    });
```
이벤트 발생시 `evtParam`에는 각 이벤트 별로 이벤트가 발생한 `시트 객체나, 행 객체, 열이름` 등이 들어 있습니다.

> **<mark>주의</mark> : 객체 생성 이후에 이벤트를 추가하는 것은 [onBeforeCreate](/docs/static/on-before-create)에서 공통으로 처리한 로직을 무시하므로 권장하지 않습니다.**

## 이벤트 파라미터(evtParam)

모든 이벤트 콜백은 **1개의 객체 파라미터**(`evtParam`)를 받습니다. 공통으로 이벤트가 발생한 시트 객체(`sheet`)와 이벤트명(`eventName`)이 들어 있으며, 이벤트에 따라 `row`(행 객체), `col`(열 이름), `value`, `x`, `y`, `keyCode` 등이 포함됩니다.

```javascript
onBeforeChange: function(evtParam) {
    evtParam.sheet;      // 이벤트가 발생한 시트 객체
    evtParam.eventName;  // 이벤트명 (예: "onBeforeChange")
    evtParam.row;        // 행 객체
    evtParam.col;        // 열 이름
    evtParam.val;        // 변경하려는 값 (이벤트마다 값 관련 파라미터명이 다름: onBeforeChange는 val)
}
```

![이벤트 파라미터(evtParam) 객체 구조](/assets/imgs/evtParam.png "onBeforeChange evtParam 예시")

## return 값으로 동작 제어

일부 이벤트는 콜백에서 값을 `return`해 동작을 제어할 수 있습니다. (자세한 동작은 각 이벤트 문서의 Return 설명 참고)

| 이벤트 | return 동작 |
|---|---|
| [onBeforeSave](./on-before-save) | `1(true)` 리턴 시 저장 작업 중단 |
| [onStartEdit](./on-start-edit) | `1(true)` 리턴 시 편집 불가 |
| [onBeforeChange](./on-before-change) | 변경할 값을 리턴하면 사용자 입력과 무관하게 그 값이 셀에 반영 |
| [onEndEdit](./on-end-edit) | `save` 인자가 `true`일 때 리턴 값으로 셀에 반영 (`true` 리턴 시 편집 유지) |

### Example
```javascript
options.Events = {
    onAfterChange :function(evtParam){
        if(evtParam.row["ConFirmYn"]=="Y"){
            alert("금월 결산이 종료되었습니다.</br>마감 정보를 확인하시고 수정해 주세요.");
        }else if(evtParam.value > evtParam.row["MaxBud"]){
            alert("입력값이 최대 예산치보다 높습니다.");
        }
    },
    onClick:function(evtParam){
        if(evtParam.col == "myBtn1"){
            if(formValidWork()){
                document.frm.submit();
            }
        }
    }
}


```

### Read More


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
