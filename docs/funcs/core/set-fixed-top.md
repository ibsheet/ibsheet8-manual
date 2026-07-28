# setFixedTop ***(method)***
> 데이터행을 상단에 고정시킵니다. 고정된 행은 `Head` 영역으로 이동합니다.  
> [DataMerge](/docs/props/cfg/data-merge)가 적용된 상태에서는 사용할 수 없으며, 머지 해제 후 고정하고 다시 머지를 적용해야 합니다.  
> [SearchMode](/docs/props/cfg/search-mode): 0, 1, 2에서만 사용할 수 있으며, 데이터행이 4행 이상이어야 합니다.

### Syntax
```javascript
boolean setFixedTop( count, render );
```

### Parameters
|Name|Type|Required| Description |
|----------|-----|---|----|
|count |`number`|<span class='optional'>선택</span>|상단에 고정시킬 데이터행의 갯수|
|render |`boolean`|<span class='optional'>선택</span>|즉시 화면 반영 여부<br/>해당 기능을 `0(false)`로 사용했을 경우, 작업 마무리 시에 `rerender()`를 실행해야 화면에 반영 됩니다.<br/>`0(false)`:반영 안함<br/>`1(true)`:즉시 반영 (`default`)|

### Return Value
***boolean*** : 설정에 대한 결과

### Example
```javascript
// 헤더행을 제외한 데이터행 4개를 상단에 고정한다.
sheet.setFixedTop(4,1);
```

### Read More
- [setFixedBottom method](./set-fixed-bottom)
- [setAutoMerge method](./set-auto-merge)
- [setAutoMergeCancel method](./set-auto-merge-cancel)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.0.0.13|`render` 인자 default 변경|
|core|8.4.0.1|`SearchMode:0` 지원|
