# PasteCols ***(cfg)***

> `Ctrl + V`로 붙여넣을 때 붙여넣기 시작 열(start column)을 설정합니다.  
> 이 속성은 열 기준 시작 위치만 제어하며,  
> 행 삽입 및 덮어쓰기 방식은 [PasteFocused](./paste-focused)에 의해 결정됩니다.

### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`0`|포커스된 열에만 붙여넣기 합니다.<br/>포커스된 셀을 기준으로 아래 방향으로 덮어씌웁니다.|
|`1`|포커스 위치와 관계없이 맨 왼쪽 보여지는 열부터 붙여넣기 합니다.<br/>`SelectingCells: 0`인 경우 기본값입니다.|
|`2`|`1`번과 동일하게 왼쪽부터 붙여넣기 하지만, 히든된 열까지 포함하여 붙여넣기 합니다.|
|`3`|포커스된 셀을 기준으로 우측 및 아래 방향으로 붙여넣기 합니다. (`default`)|


### Example
```javascript
options = {
    Cfg :{
      PasteCols: 1 // 맨 왼쪽 보여지는 열부터 붙여넣기
    }
};
```

### Read More
- [PasteFocused cfg](./paste-focused)
- [CanCopyPaste col](/docs/props/col/can-copy-paste)
- [SelectingCells cfg](./selecting-cells)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|