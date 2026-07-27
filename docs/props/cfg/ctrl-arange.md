# CtrlARange ***(cfg)***

> `Ctrl + A` 단축키로 시트 전체를 선택할 때  
> **데이터 영역만 선택할지** 또는 **Header와 Foot 영역까지 포함하여 선택할지** 설정합니다.
>
> 기본적으로는 데이터 영역만 선택됩니다.  
> `CtrlARange: true`로 설정하면 Header와 Foot 행도 선택 대상에 포함됩니다.  
>
> 단, Header 또는 Foot 행에 `CanSelect: true`가 설정되어 있어야 선택됩니다.

<!-- synonyms: ctrl a range, select all range, header selection, footer selection, 전체 선택 범위, ctrl+a 범위 -->

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0` (`false`)|`Ctrl + A` 시 데이터 영역만 선택 (`default`)|
|`1` (`true`)|`Ctrl + A` 시 데이터 영역 + Header, Foot 영역까지 포함하여 선택|


### Example
```javascript
options.Def = {
    Header: {
        CanSelect: true
    },
    Foot: {
        CanSelect: true
    },
};
options.Cfg = {
    CtrlARange: true        // Ctrl + A 시 Header와 Foot까지 포함하여 선택
};
```
### 참고
- `CtrlARange`는 **선택 범위(selection range)**에만 영향을 줍니다.
- 실제 복사 범위는 `CopyCols` 설정에 따라 결정됩니다.

### Read More
- [CopyCols cfg](./copy-cols)
- [CanSelect cfg](./can-select)
- [CanSelect col](/docs/props/col/can-select)
- [CanSelect row](/docs/props/row/can-select)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.23|기능 추가|
