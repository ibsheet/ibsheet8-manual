# IgnoreFocused ***(cfg)***

<!-- synonyms: 포커스, 자동 포커스, 포커스 제거, 포커스 안줌, focus, auto focus, remove focus, 조회 후 스크롤 이동, scroll jump after search, 조회 후 커서 사라짐, 입력 포커스 뺏김, input focus lost, 조회 후 첫 행 선택, 첫 셀 포커스, first cell focus, master-detail 포커스 유지, 마스터 디테일, 포커스 테두리, focus layer -->

> 조회([doSearch](/docs/funcs/core/do-search), [loadSearchData](/docs/funcs/core/load-search-data))가 끝나면 시트는 첫 번째 셀에 자동으로 포커스를 둡니다. 이 자동 포커스를 어떻게 할지 설정합니다.  
> `1`로 설정하면 포커스를 두지 않습니다.  
> `2`로 설정하면 첫 셀에 포커스 표시(선택 테두리)만 하고, 방향키/Tab 이동은 동작하지 않습니다.  
> `master-detail` 구조에서 다른 시트의 포커스를 유지할 때 적합합니다.  
> `1`, `2`는 조회 후 브라우저 스크롤이 시트 쪽으로 이동하는 것도 막습니다.  
> 탭 이동 후의 스크롤 이동은 [ScrollFreeze](/docs/props/cfg/scrollFreeze)를 참고합니다.  
> 자동 포커스는 행([CanFocus row](/docs/props/row/can-focus))과 열([CanFocus col](/docs/props/col/can-focus))이 모두 `CanFocus:1`인 셀 중 첫 셀에 둡니다.  
> [onFocus](/docs/events/on-focus) 이벤트는 `0`, `2`에서만 발생합니다.

### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`0`|조회 후 행/열이 모두 `CanFocus:1`인 첫 셀로 포커스 + 방향키/Tab 이동 가능, `onFocus` 이벤트 발생 (`default`)|
|`1`|조회 후 포커스를 두지 않음, `onFocus` 이벤트 발생 안 함|
|`2`|조회 후 행/열이 모두 `CanFocus:1`인 첫 셀로 포커스, 방향키/Tab 이동 불가, `onFocus` 이벤트 발생|

### Example
```javascript
// 조회 후 시트에 포커스를 두지 않음
options.Cfg = {
    IgnoreFocused: 1
};

// master-detail 구조 — detail 시트 조회 후에도 master 시트의 포커스 유지
options.Cfg = {
    IgnoreFocused: 2
};
```

#### 동작 비교

> 아래 화면은 input에 커서가 있는 상태로 시트를 조회한 모습입니다 (옵션 동작 자체는 input 없이도 동일).

- `0` (default) : 시트로 포커스가 이동합니다. input의 커서는 사라지고, 첫 셀에 포커스가 표시되며 방향키/Tab 이동이 가능합니다.  
  ![IgnoreFocused 0](/assets/imgs/ignoreFocused0.png "IgnoreFocused 0")

- `1` : input의 커서가 유지되고, 시트에는 포커스가 표시되지 않습니다.  
  ![IgnoreFocused 1](/assets/imgs/ignoreFocused1.png "IgnoreFocused 1")

- `2` : input의 커서가 유지되고, 시트에는 포커스 표시만 됩니다. 시트에서 방향키/Tab 이동은 동작하지 않습니다.  
  ![IgnoreFocused 2](/assets/imgs/ignoreFocused2.png "IgnoreFocused 2")

### Read More
- [focus method](/docs/funcs/core/focus)
- [blur method](/docs/funcs/core/blur)
- [onFocus event](/docs/events/on-focus)
- [CanFocus row](/docs/props/row/can-focus)
- [CanFocus col](/docs/props/col/can-focus)
- [doSearch method](/docs/funcs/core/do-search)
- [loadSearchData method](/docs/funcs/core/load-search-data)
- [ScrollFreeze cfg](/docs/props/cfg/scrollFreeze)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.4.0.1|옵션 `2` 추가|
