# setAutoMerge ***(method)***

> 시트 생성 후 [DataMerge](/docs/props/cfg/data-merge), [HeaderMerge](/docs/props/cfg/header-merge) 등 Cfg에 설정한 병합 옵션을 동적으로 변경합니다.  
> 호출 시 Cfg의 병합 관련 설정값이 초기화되며, 전달한 파라미터만 적용됩니다. 전달하지 않은 옵션은 기본값으로 초기화됩니다.  
> [setFixedTop](./set-fixed-top)/[setFixedBottom](./set-fixed-bottom)으로 고정한 행은 `Head`/`Foot` 영역으로 바뀌어 병합이 적용되지 않으므로, `headMerge`/`footMerge`를 별도로 설정해야 합니다.  
> `SEQ` 열에 대해서는 병합을 실행하지 않습니다.

### Syntax
```javascript
void setAutoMerge( dataMerge, headerMerge, prevColumnMerge, fixPrevColumnMerge, headMerge, footMerge, headPrevColumnMerge, footPrevColumnMerge );
```

### Parameters
|Name|Type|Required| Description |
|----------|-----|---|----|
|dataMerge|`number`|<span class='optional'>선택</span>|데이터 영역의 셀들을 병합할 때 적용할 기준<br/>`0`:병합 안함 (`default`)<br/>`1`:열 기준 병합<br/>`2`:행 기준 병합<br/>`3`:열 우선 병합<br/>`4`:행 우선 병합<br/>`5`:열 우선 사방 병합<br/>`6`:행 우선 사방 병합|
|headerMerge|`number`|<span class='optional'>선택</span>|헤더 영역의 셀들을 병합할 때 적용할 기준<br/>`0`:병합 안함 (`default`)<br/>`1`:열 기준 병합<br/>`2`:행 기준 병합<br/>`3`:열 우선 병합<br/>`4`:행 우선 병합<br/>`5`:열 우선 사방 병합<br/>`6`:행 우선 사방 병합|
|prevColumnMerge|`number`|<span class='optional'>선택</span>|앞 열 기준으로 셀 병합할 지 여부<br/>`0`:전체영역에 앞컬럼 머지기능을 사용안함 (`default`)<br/>`1`:데이터 영역에만 앞컬럼머지기능을 사용<br/>`2`:헤더영역에서만 앞컬럼머지기능을 사용<br/>`3`:데이터 및 헤더 영역에서 앞컬럼머지 기능 사용<br/>|
|fixPrevColumnMerge|`string`|<span class='optional'>선택</span>|병합의 기준이 될 열의 `Name` (`default: 0`)|
|headMerge|`number`|<span class='optional'>선택</span>|`Head` 영역의 셀들을 병합할 때 적용할 기준<br/>`0`:병합 안함 (`default`)<br/>`1`:열 기준 병합<br/>`2`:행 기준 병합<br/>`3`:열 우선 병합<br/>`4`:행 우선 병합<br/>`5`:열 우선 사방 병합<br/>`6`:행 우선 사방 병합|
|footMerge|`number`|<span class='optional'>선택</span>|`Foot` 영역의 셀들을 병합할 때 적용할 기준<br/>`0`:병합 안함 (`default`)<br/>`1`:열 기준 병합<br/>`2`:행 기준 병합<br/>`3`:열 우선 병합<br/>`4`:행 우선 병합<br/>`5`:열 우선 사방 병합<br/>`6`:행 우선 사방 병합|
|headPrevColumnMerge|`boolean`|<span class='optional'>선택</span>| `Head`의 고정행 영역에서 앞 열 기준으로 셀 병합할 지 여부<br>`0(false)`:`Head`의 고정행 영역에서 앞 열 기준으로 셀 병합 사용 안함 (`default`)<br>`1(true)`:`Head`의 고정행 영역에서 앞 열 기준으로 셀 병합 사용|
|footPrevColumnMerge|`boolean`|<span class='optional'>선택</span>| `Foot`의 고정행 영역에서 앞 열 기준으로 셀 병합할 지 여부<br>`0(false)`:`Foot`의 고정행 영역에서 앞 열 기준으로 셀 병합 사용 안함 (`default`)<br>`1(true)`:`Foot`의 고정행 영역에서 앞 열 기준으로 셀 병합 사용|

### Return Value
***none***

### Example
```javascript
// Cfg에 DataMerge:3, HeaderMerge:2, PrevColumnMerge:1 설정된 상태에서
// dataMerge만 전달하면 HeaderMerge, PrevColumnMerge는 0으로 초기화됨
sheet.setAutoMerge({dataMerge: 1});

// Cfg 설정을 유지하면서 변경하려면 모든 옵션을 전달해야 함
sheet.setAutoMerge({dataMerge: 1, headerMerge: 2, prevColumnMerge: 1});

// setFixedTop 사용 시 머지 해제 → 고정 → 다시 머지 적용 (병합 해제/재적용으로 성능 저하 가능)
sheet.setAutoMergeCancel();
sheet.setFixedTop(3);
sheet.setAutoMerge({dataMerge: 3, headMerge: 3});
```


### Read More
- [DataMerge cfg](/docs/props/cfg/data-merge)
- [HeaderMerge cfg](/docs/props/cfg/header-merge)
- [PrevColumnMerge cfg](/docs/props/cfg/prev-column-merge)
- [FixPrevColumnMerge cfg](/docs/props/cfg/fix-prev-column-merge)
- [MergeCellsMatch cfg](/docs/props/cfg/merge-cells-match)
- [setAutoMergeCancel method](./set-auto-merge-cancel)
- [setFixedTop method](./set-fixed-top)
- [setFixedBottom method](./set-fixed-bottom)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.0.0.15|`fixPrevColumnMerge`추가|
|core|8.2.0.14|`headMerge`, `footMerge`, `headPrevColumnMerge`, `footPrevColumnMerge` 추가|