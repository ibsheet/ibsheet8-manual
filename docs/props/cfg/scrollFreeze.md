# ScrollFreeze ***(cfg)***

<!-- synonyms: ScrollFreeze, scroll freeze, freeze browser scroll, body overflow hidden, 브라우저 스크롤 고정, 스크롤 이동 방지, body overflow, 스크롤 프리즈, 조회 후 스크롤 유지, 화면 스크롤 고정, 탭 전환 스크롤, iframe 탭, 탭 복귀 스크롤, 멀티탭 스크롤 이동, 탭 이동 시 스크롤, 스크롤 튐, 스크롤 자동 이동, scroll jump, 포커스 셀로 스크롤 이동, 그리드로 스크롤 이동, div 스크롤 이동, 페이지 스크롤 이동, 조회 후 스크롤 이동, scrollIntoView -->

> 시트가 들어 있는 페이지의 브라우저 스크롤이나, 시트를 담은 div의 스크롤이 포커스된 셀 위치로 저절로 이동하지 않도록 막는 기능입니다.  
> `body` 태그에 `overflow:hidden;` 을 사용했을 때, 조회 후 브라우저 스크롤을 이동시키고 싶지 않은 경우에 사용할 수 있습니다.  
> 주로 다음 두 경우에 스크롤이 이동합니다.
> - 조회가 끝나고 시트가 첫 셀에 자동으로 포커스를 줄 때
> - 탭을 이동했다 돌아와서, 포커스가 남아 있던 셀이 다시 보일 때

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|기능 사용 안 함 (`default`)|
|`1(true)`|기능 사용|

### Example

시트 전체에 적용합니다. 조회 후나 탭 복귀 시 포커스 때문에 브라우저 스크롤이 이동하지 않습니다.
```javascript
options.Cfg = {
  ScrollFreeze: 1
};
```

특정 조회에서만 적용합니다. 조회가 끝난 뒤 되돌려야 하므로 `sync:1`(동기)로 조회합니다.
```javascript
sheet.ScrollFreeze = 1;
sheet.loadSearchData({ data: DATA, sync: 1 });
sheet.ScrollFreeze = 0;
```

#### IgnoreFocused와의 차이

|상황|[IgnoreFocused](/docs/props/cfg/ignore-focused) `1`|[IgnoreFocused](/docs/props/cfg/ignore-focused) `2`|`ScrollFreeze` `1`|
|---|---|---|---|
|조회 후 스크롤 이동|막힘 (포커스 없음)|막힘 (포커스 표시만, 방향키/Tab 이동 안 됨)|막힘 (`IgnoreFocused` 기본값 `0`이어도 막힘, 포커스는 그대로)|
|탭 복귀 후 스크롤 이동|못 막음|못 막음|막음|

조회 후 스크롤 이동만 막으면 된다면 `IgnoreFocused`로도 충분하고, 탭 복귀 시 이동까지 막으려면 `ScrollFreeze`를 사용합니다.

### Read More
- [IgnoreFocused cfg](/docs/props/cfg/ignore-focused)
- [focus method](/docs/funcs/core/focus)
- [blur method](/docs/funcs/core/blur)

### Since

|product|version|desc|
|---|---|---|
|core|8.1.0.45|기능 추가|
|core|8.1.0.61|기능 변경|
