# setAllCheck ***(method)***

<!-- synonyms: 전체 체크 함수, 일괄 체크, 헤더 체크 호출, all check method, 코드로 전체 체크 -->

> `Bool` 타입의 열 전체를 체크/체크해제합니다.  
> 편집 불가능한 셀은 일괄 처리에서 제외됩니다. (편집 불가 셀까지 체크하려면 [setValue](./set-value)를 사용하세요)  
> 사용자 클릭이 아닌 코드 호출이므로 [HeaderCheckPageOnly](/docs/props/cfg/header-check-page-only)와 [AllCheckIgnoreEvent](/docs/props/col/all-check-ignore-event) 설정은 적용되지 않습니다. (페이징과 무관하게 모든 행이 대상이며, `onAfterChange` 이벤트도 행마다 발생합니다)  
> 이벤트를 차단하려면 `ignoreEvent` 인자를 `true`로 지정하세요.

### Syntax
```javascript
void setAllCheck( col, val, ignoreEvent );
```

### Parameters
|Name|Type|Required| Description |
|----------|-----|---|----|
|col |`string`|<span class='required'>필수</span>|열이름|
|val |`boolean`|<span class='required'>필수</span>|체크 여부<br>`0(false)`: 체크해제<br>`1(true)`: 체크|
|ignoreEvent|`boolean`|<span class='optional'>선택</span>|`onAfterChange` 이벤트 발생 여부<br>`0(false)`: 이벤트 발생 (`default`)<br>`1(true)`: 이벤트 발생 안 함|

### Return Value
***none***

### Example
```javascript
// "CHK" 열 전체 체크
sheet.setAllCheck("CHK", 1);

// "CHK" 열 전체 체크해제 + onAfterChange 이벤트 차단 (대량 처리 시 성능 향상)
sheet.setAllCheck("CHK", 0, true);
```

### Read More
- [setCheck method](./set-check)
- [HeaderCheck cfg](/docs/props/cfg/header-check)
- [HeaderCheck col](/docs/props/col/header-check)
- [HeaderCheckPageOnly cfg](/docs/props/cfg/header-check-page-only)
- [AllCheckIgnoreEvent col](/docs/props/col/all-check-ignore-event)
- [onBeforeCheckAll event](/docs/events/on-before-check-all)
- [onCheckAllFinish event](/docs/events/on-check-all-finish)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.0.0.7|ignoreEvent 인자 추가|
