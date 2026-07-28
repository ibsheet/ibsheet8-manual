# hideCol ***(method)***
> 특정 열을 감춥니다. 
>
> 여러 컬럼을 `hide` 할시 `render` 인자를 `false` 로 하여 작업 후에는 `rerender` 를 무조건 호출하셔야 합니다.

### Syntax
```javascript
void hideCol( col, userHidden, merge, render );
```

### Parameters


|Name|Type|Required| Description |
|----------|-----|---|----|
|col|`string`|<span class='required'>필수</span>|감추고자 하는 열이름|
|userHidden|`boolean`|<span class='optional'>선택</span>|사용자 숨김 플래그 설정 여부<br>`0(false)`: 개발자 숨김 — 개인화 복원 대상이 아님 (`default`)<br>`1(true)`: 사용자 숨김 — 개인화 복원 대상. [getCurrentInfo](./get-current-info) 결과에 `UserHidden:1`로 표시됨|
|merge|`boolean`|<span class='optional'>선택</span>| 열을 숨기면서 자동 머지합니다.<br/> <span style='color:red'>많은 데이터가 있는 시트에서 실행 시 느려질 수 있습니다.</span><br>`0(false)`:병합 실행 안함 (`default`)<br>`1(true)`:병합 실행|
|render|`boolean`|<span class='optional'>선택</span>|즉시 화면 반영 여부<br/>해당 기능을 `0(false)`로 사용했을 경우, 작업 마무리 시에 `rerender()`를 실행해야 화면에 반영 됩니다.<br/>`0(false)`:반영 안함<br/>`1(true)`:즉시 반영 (`default`)|

### Return Value
***none***

### Example
```javascript
//CPT_NM 열을 감춥니다.
sheet.hideCol( "CPT_NM" );


//AMT 열을 감추면서 사용자 감춤여부를 설정합니다.
sheet.hideCol( "AMT" , 1 );

// render 인자를 사용합니다.
sheet.hideCol( { col: "AMT", render: false } );
sheet.rerender();

```

### Read More
- [getCurrentInfo method](./get-current-info)
- [saveCurrentInfo method](./save-current-info)
- [showCol method](./show-col)
- [onShowColumn event](/docs/events/on-show-column)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.0.0.6|`merge` 인자 추가|
|core|8.0.0.17|`render` 인자 추가|