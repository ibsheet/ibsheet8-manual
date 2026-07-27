# endEdit ***(method)***

<!-- synonyms: 편집 종료, 편집 중지, 편집 반영, edit end, endedit -->

> 셀의 편집 상태를 종료합니다.  
> `save: 1`이면 수정한 값을 시트에 반영하고, `save: 0`(default)이면 수정 내용을 폐기합니다.  
> 호출 시 [onEndEdit](/docs/events/on-end-edit) 이벤트가 발생합니다.

### Syntax
```javascript
mixed endEdit(save);
```

### Parameters

|Name|Type|Required|Description|
|----------|-----|---|----|
|save|`boolean`|<span class='optional'>선택</span>|편집 종료시 현재 값을 반영할지 여부를 설정합니다.<br>`0(false)`:수정 중인 데이터를 반영하지 않고 편집 상태를 종료 (`default`)<br>`1(true)`:수정 중인 데이터를 반영하며 편집 상태를 종료|

### Return Value
***mixed***

|returnValue|Description|
|---|---|
|`null`|편집 중이 아닌 경우|
|`0(false)`|값에 변화가 없는 경우 (`save: 0`으로 폐기되었거나, `save: 1`이지만 기존값과 동일)|
|`1(true)`|정상적으로 편집한 값이 반영됨 (`save: 1`)|
|`-1`|수정한 값에 문제가 있어 편집이 종료되지 못한 경우 (잘못된 날짜 입력 등)|


### Example
```javascript
// 편집 종료 + 변경 반영
sheet.endEdit(1);

// 편집 종료 + 변경 폐기 (default)
// 예: 원래값 "abc" → 편집 중 "9999" → endEdit() 호출 → "abc"로 복원, false 리턴
sheet.endEdit();
```

### Read More

- [startEdit method](./start-edit)
- [focus method](./focus)
- [onEndEdit event](/docs/events/on-end-edit)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
