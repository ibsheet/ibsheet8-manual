# showHint ***(method)***
> 셀의 힌트를 활성화 합니다.

###
![힌트활성화](/assets/imgs/hint1.png "마우스 커서가 셀에 올라갔을때 힌트를 통해 감춰진 부분이 보여짐")<br/>
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
|staticMode|`boolean`|<span class='optional'>선택</span>|`0(false)` : 시트 위로 마우스 커서가 올라가면(헤더든 데이터든) 기존 활성화 되었던 힌트가 비활성화 됨. (`default`)<br/>`1(true)` : 마우스 커서와 무관하게 다른 셀에서 힌트가 활성화 되었을 때, 기존 힌트가 비활성화 됨.

### Return Value
***boolean*** : 힌트가 활성화 되면 `true`, 활성화 되지 않으면 `false`

### Example
```javascript
var r5 = sheet.getRowById("AR8");
//AR8 행 "CPT_WASH_TI_NM" 열에 힌트를 보여준다.
sheet.showHint(r5, "CPT_WASH_TI_NM");
```

### Read More

- [hideHint method](./hide-hint)
- [onHint event](/docs/events/on-show-hint)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.0.0.1|인자명 변경(`static`->`staticMode`)|
