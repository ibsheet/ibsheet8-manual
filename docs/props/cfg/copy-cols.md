# CopyCols ***(cfg)***

> 시트에서 데이터를 복사할 때 **복사 범위를 결정하는 방식(copy range rule)을 설정합니다.**  
> 선택 방식(`SelectingCells`)과 포커스 위치에 따라 실제 복사 범위가 결정됩니다.

<!-- synonyms: copy columns, copy mode, clipboard copy range, 복사 기준, 복사 범위 설정 -->

### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`0`|선택 범위와 관계없이 **포커스 기준으로 복사**<br/>- 범위 선택이 없으면 **포커스된 셀 1개만 복사**<br/>- 범위를 선택해도 **포커스된 열의 범위만 복사**|
|`1`|선택 범위가 있으면 선택된 셀 범위만 복사, 없으면 **포커스된 행의 모든 표시 열 복사**<br/>`SelectingCells: 0`인 경우 기본값입니다.|
|`2`|`1`번과 동일하나, **숨겨진 열까지 포함하여 복사**|
|`3`|선택 범위가 있으면 선택된 셀 범위만 복사, 없으면 **포커스된 셀 1개만 복사** (`default`)|

### Example
```javascript
options = {
    Cfg:{
      CopyCols: 1  // 선택 범위가 없으면 포커스 행 전체(표시 열) 복사, 선택 범위가 있으면 해당 범위만 복사
    }
};
```

### Read More
- [CanCopyPaste col](/docs/props/col/can-copy-paste)
- [CopyEdit cfg](./copy-edit)
- [CopyValue cell](/docs/props/cell/copy-value)
- [NoCRLF cfg](/docs/props/cfg/no-crlf)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
