# MaximumValue/MinimumValue 마이그레이션

<!-- synonyms: IBSheet7, 마이그레이션, sheet7, migration, v7, v8, ibsheet7에서 ibsheet8로, MaximumValue, MinimumValue, 최대값, 최소값, max value, min value, 값 제한, value limit -->

[IBSheet.onBeforeCreate](../static/on-before-create) 이벤트에서 [onEndEdit](../events/on-end-edit) 이벤트를 공통 정의 함으로써 구현 가능합니다. 

아래 내용을 참고해 주세요.
1. ibsheet-common.js 에 onBeforeCreate 이벤트를 다음과 같이 정의 합니다.
```js
_IBSheet.onBeforeCreate = function(init) {
    //event 공통 정의
    init.options.Events = init.options.Events || {};
    
    // 개별 화면에서 선언한 onEndEdit가 있는 경우, orgEndEdit에 저장
    if(typeof init.options.Events.onEndEdit != "undefined") {
      init.options.Events.orgEndEdit = init.options.Events.onEndEdit;
    }

    // onEndEdit 이벤트 공통 정의
    init.options.Events.onEndEdit = function(evt) {
      // 컬럼에 MinimumValue 가 정의 돈 경우
      if (typeof evt.sheet.Cols[evt.col].MinimumValue != "undefined") {
        if (evt.sheet.Cols[evt.col].MinimumValue > Number(evt.raw)) {
          alert(
            "입력 가능한 최소값은" +
              evt.sheet.Cols[evt.col].MinimumValue +
              "입니다."
          );
          // 편집창을 빠져나가지 못하게 함
          return true;
        }
      }

      // 컬럼에 MaximumValue가  정의 된 경우
      if (typeof evt.sheet.Cols[evt.col].MaximumValue != "undefined") {
        if (evt.sheet.Cols[evt.col].MaximumValue < Number(evt.raw)) {
          alert(
            "입력 가능한 최대값은" +
              evt.sheet.Cols[evt.col].MaximumValue +
              "입니다."
          );
          return true;
        }
      }

      // 개별화면에서 정의한 onEndEidt가 있는 경우
      if(typeof init.options.Events.orgEndEdit != "undefined") {
        return init.options.Events.orgEndEdit(evt)
      }
    }
    return init;
  }
```
 
2. 시트 생성시 IBSheet7 제품과 동일하게 MaximumValue, MinimumValue를 정의하여 사용합니다.
```js
const initSheet = {
    Cols:[
        {Header:"이익", Type: "Int", Name:"income", MinimumValue:1000 }, // 값은 1000 이상 입력 가능
        {Header:"손해", Type: "Int", Name:"loss", MaximumValue:0 }  // 값은 0 이하 입력 가능
        ...
    ]
}
IBSheet.create({
    id: "mySheet",
    el: "sheetDIV",
    options: initSheet
})

```
