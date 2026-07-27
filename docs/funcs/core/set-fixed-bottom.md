# setFixedBottom ***(method)***
> 맨 아래 데이터행부터 `count`만큼 하단 `Foot` 영역에 고정시킵니다.  
> [DataMerge](/docs/props/cfg/data-merge)가 적용된 상태에서는 사용할 수 없으며, 머지 해제 후 고정하고 다시 머지를 적용해야 합니다.  
> 고정행의 갯수가 시트 높이를 초과하면 기능이 제한됩니다.  
> [SearchMode](/docs/props/cfg/search-mode): 0, 1, 2에서만 사용할 수 있습니다.


### Syntax
```javascript
boolean setFixedBottom( count, render );
```

### Parameters
|Name|Type|Required| Description |
|----------|-----|---|----|
|count |`number`|<span class='optional'>선택</span>|하단에 고정시킬 데이터행의 갯수|
|render |`boolean`|<span class='optional'>선택</span>|즉시 화면 반영 여부<br/>해당 기능을 `0(false)`로 사용했을 경우, 작업 마무리 시에 `rerender()`를 실행해야 화면에 반영 됩니다.<br/>`0(false)`:반영 안함<br/>`1(true)`:즉시 반영 (`default`)|

### Return Value
***boolean*** : 설정에 대한 결과

### Example
```javascript
// 맨 아래 데이터 행부터 시작해서 데이터행 4개를 하단에 고정한다.
sheet.setFixedBottom(4,1);
```

### Read More
- [setFixedTop method](./set-fixed-top)
- [setAutoMerge method](./set-auto-merge)
- [setAutoMergeCancel method](./set-auto-merge-cancel)

### Since

|product|version|desc|
|---|---|---|
|core|8.1.0.23|기능 추가|
|core|8.4.0.1|`SearchMode:0` 지원|
