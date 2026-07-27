# ControlsTag ***(cfg)***
> 시트에서 사용하는 팝업 메뉴, 툴팁, 메시지, 힌트 등의  
> 표시 기준이 되는 부모 태그를 지정합니다.
>
> 설정하지 않을 경우, 해당 요소들은 기본적으로 `document.body`에 생성됩니다.
>
> ShadowDOM 환경(Lightning Web Component 등)처럼  
> `document.body`를 기준 영역으로 사용할 수 없는 경우에는  
> 시트가 포함된 컴포넌트 내부에 별도의 `div`를 생성하고  
> 해당 요소를 `ControlsTag`로 지정해야 합니다.

<!-- synonyms: controls tag, popup container, dialog container, tooltip parent, shadow dom popup, lwc popup 영역 -->

### 주의사항

- `ControlsTag`는 **시트 생성 시에만 설정 가능**하며, 이후 변경할 수 없습니다.
- 반드시 시트의 DIV와 **동일한 컴포넌트 영역 내부**에 존재해야 합니다.
- 시트가 렌더링되는 컴포넌트 외부(상위 영역)에 위치해서는 안됩니다.
- 생성 시 다음 스타일이 필요합니다:  
  `position:absolute; left:0; top:0;`

### Type
`HTMLElement`

### Options
|Value|Description|
|-----|-----|
|`HTMLElement`|팝업/툴팁/메시지 등의 표시 기준이 되는 부모 요소|

### Example
```html

<template>
  <lightning-card>
    <div>
      <!-- 팝업/툴팁 표시 기준 영역 -->
      <div class="IBControls" 
           style="position:absolute;left:0px;top:0px;"  
           lwc:dom="manual"></div> 
      <!-- 시트 영역 -->
      <div class="sheetDiv" 
           style="width: 100%;height: 400px;" 
           lwc:dom="manual"></div>
    </div>
  </lightning-card>
</template>
```


```javascript
// 시트 내 팝업 메뉴, 툴팁, 메시지, 힌트를 띄울 위치를 설정하기 위한 부모 태그 설정
options.Cfg = {
   ControlsTag: this.template.querySelector(".IBControls") 
};
```

### Read More
- [DialogsArea cfg](/docs/props/cfg/dialogs-area)
- [IBSheet.QuerySelector static](/docs/static/query-selector)

### Since

|product|version|desc|
|---|---|---|
|core|8.3.0.0|기능 추가|
