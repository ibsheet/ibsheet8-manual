# DialogsArea ***(cfg)***
> 시트 내 다이얼로그가 표시될 **기준 영역(container)** 을 지정합니다.  
>
> Salesforce의 Lightning Web Component(LWC) 또는 Shadow DOM 환경처럼  
> `document.body` 전체가 아닌 **페이지 내 특정 컴포넌트 영역을 다이얼로그 기준 영역으로 사용해야 하는 경우**,  
> 해당 컴포넌트의 body에 해당하는 영역을 `(Cfg) DialogsArea`로 설정할 수 있습니다.
>
> `DialogsArea`는 반드시 **시트가 생성된 동일한 컴포넌트 영역 내부**에 있어야 하며,  
> 시트가 생성되는 컴포넌트보다 **상위 컴포넌트 영역을 지정할 수 없습니다.**


### Type
`object`

### Options
|Value|Description|
|-----|-----|
|`object`|시트 내 다이얼로그의 기준 영역|

### Example
```javascript

<template>
  <lightning-card> <!-- LWC 컴포넌트에서 Body에 해당하는 영역 -->
    <div>
      <div class="IBControls" lwc:dom="manual"></div>
      <div class="sheetDiv" style="width: 100%; height: 400px;" lwc:dom="manual"></div>
    </div>
  </lightning-card>
</template>

...

options.Cfg = {
   DialogsArea: this.template.firstChild, // lightning-card 태그를 시트 내 다이얼로그의 위치를 설정하기 위한 영역으로 지정
};
```

### Read More
- [ControlsTag cfg](/docs/props/cfg/controls-tag)
- [IBSheet.QuerySelector static](/docs/static/query-selector)

### Since

|product|version|desc|
|---|---|---|
|core|8.3.0.0|기능 추가|
