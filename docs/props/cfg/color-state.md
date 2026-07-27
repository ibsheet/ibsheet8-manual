# ColorState ***(cfg)***
> 행/셀 상태에 따라 자동으로 표시되는 배경색 사용 여부를 설정합니다.  
> `ColorState`는 bit 연산 방식입니다.  
> 기본값은 `63` 입니다.

<!-- synonyms: color state, cell state color, changed color, read only color, error color, 상태 색상, 배경색 설정, 수정 색상 -->


### Type
`number`

### Options
|Value|Description|Class|
|-----|-----|---|
|`0`|모든 상태(행/셀 변경, 읽기전용, Formula, 오류 등)에 대한 배경색 표시 안함||
|`1`|값이 변경된 **셀에만** 배경색 표시|`.IBColorChangedCell`|
|`2`|행이 `추가`(`Added`), `수정`(`Changed`), `삭제`(`Deleted`) 상태일 때 행 전체에 배경색 표시|`.IBColorAdded`, `.IBColorChanged`, `.IBColorDeleted`|
|`4`|추가/삭제된 열에 대한 배경색 표시|`.IBColorAdded`, `.IBColorDeleted`|
|`8`|`CanEdit`, `CanFocus`가 `false`인 셀 배경색 표시|`.IBColorReadOnly`, `.IBColorNoFocus`|
|`16`|`Formula`가 설정된 셀 배경색 표시|`.IBColorReadOnly`|
|`32`|`ValidCheck`에 의해 오류가 발생한 셀 배경색 표시|`.IBColorError`|

### Example
```javascript
options.Cfg = {
   "ColorState": 7  // 1 + 2 + 4 (셀 수정, 행 상태, 열 상태 색상 표시)
};
```

### Read More
- [NoColor row](/docs/props/row/no-color)
- [Added row](/docs/props/row/added)
- [Changed row](/docs/props/row/changed)
- [Deleted row](/docs/props/row/deleted)
- [CanEdit cfg](/docs/props/cfg/can-edit)
- [CanFocus col](/docs/props/col/can-focus)
- [Formula col](/docs/props/col/formula) 
- [ValidCheck cfg](./valid-check)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
