# IgnoreFocused ***(cfg)***

<!-- synonyms: 포커스, 자동 포커스, 포커스 제거, 포커스 안줌, focus, auto focus, remove focus -->

> 시트는 데이터 조회([doSearch](/docs/funcs/core/do-search), [loadSearchData](/docs/funcs/core/load-search-data)) 후 행([CanFocus row](/docs/props/row/can-focus)) / 열([CanFocus col](/docs/props/col/can-focus))이 모두 `CanFocus:1`인 첫 셀에 자동으로 포커스를 둡니다.  
> `1`로 설정하면 포커스를 설정하지 않습니다.  
> `2`로 설정하면 포커스 레이어만 표시되고 방향키/Tab 이동은 동작하지 않습니다.  
> 여러 시트가 포커스로 연결된 `master-detail` 구조에서 다른 시트의 포커스를 유지할 때 적합합니다.  
> [onFocus](/docs/events/on-focus) 이벤트는 `0`/`2`에서만 발생합니다.

### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`0`|조회 후 행/열이 모두 `CanFocus:1`인 첫 셀로 포커스 + 방향키/Tab 이동 가능, `onFocus` 이벤트 발생 (`default`)|
|`1`|조회 후 포커스 레이어 표시 없음, `onFocus` 이벤트 발생 안 함|
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

- `0` (default)  
  ![IgnoreFocused 0](/assets/imgs/ignoreFocused0.png "IgnoreFocused 0")

- `1`  
  ![IgnoreFocused 1](/assets/imgs/ignoreFocused1.png "IgnoreFocused 1")

- `2`  
  ![IgnoreFocused 2](/assets/imgs/ignoreFocused2.png "IgnoreFocused 2")

### Read More
- [focus method](/docs/funcs/core/focus)
- [blur method](/docs/funcs/core/blur)
- [onFocus event](/docs/events/on-focus)
- [CanFocus row](/docs/props/row/can-focus)
- [CanFocus col](/docs/props/col/can-focus)
- [doSearch method](/docs/funcs/core/do-search)
- [loadSearchData method](/docs/funcs/core/load-search-data)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.4.0.1|옵션 `2` 추가|
