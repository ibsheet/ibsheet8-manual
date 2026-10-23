# showHint ***(method)***

<!-- synonyms: showHint, show-hint, 힌트, 힌트 표시, 힌트 띄우기, 코드로 힌트 표시, 힌트 고정, staticMode, 셀 힌트, 툴팁, hint, show hint, tooltip -->

> 지정한 셀에 힌트를 표시합니다.  
> 마우스 커서를 셀에 올리지 않아도 코드로 힌트를 띄울 때 사용하며, 표시된 힌트는 [hideHint](./hide-hint)로 감출 수 있습니다.  
> 마우스를 올렸을 때와 같은 조건으로 표시되므로, 셀 내용이 잘리지 않은 셀에는 힌트가 표시되지 않고 `false`를 리턴합니다.

###
![힌트활성화](/assets/imgs/hint1.png "마우스 커서가 셀에 올라갔을 때 힌트를 통해 감춰진 부분이 보여짐")<br/>
[힌트 예시]

### Syntax
```javascript
boolean showHint( row, col, staticMode );
```

### Parameters
|Name|Type|Required| Description |
|----------|-----|---|----|
|row |`object`|<span class='required'>필수</span>|[데이터 로우 객체](/docs/appx/row-object)|
|col |`string`|<span class='required'>필수</span>|열이름|
|staticMode|`boolean`|<span class='optional'>선택</span>|`0(false)` : 시트 위로 마우스 커서가 올라가면(헤더와 데이터 영역 모두) 표시된 힌트가 사라짐 (`default`)<br/>`1(true)` : 마우스 커서와 무관하게, 다른 셀에 힌트가 표시될 때 기존 힌트가 사라짐|

### Return Value
***boolean*** : 힌트가 표시되면 `true`, 표시되지 않으면 `false`

### Example
```javascript
var row = sheet.getRowById("AR8");
//AR8 행 "CPT_WASH_TI_NM" 열에 힌트를 보여준다.
sheet.showHint(row, "CPT_WASH_TI_NM");
```

### Read More

- [hideHint method](./hide-hint)
- [onShowHint event](/docs/events/on-show-hint)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.0.0.1|인자명 변경(`static`->`staticMode`)|
