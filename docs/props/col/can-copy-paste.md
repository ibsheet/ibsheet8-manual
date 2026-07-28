# CanCopyPaste ***(col)***
> 해당 열의 `Ctrl + C` 복사와 `Ctrl + V` 붙여넣기 동작을 제한합니다.  

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|복사/붙여넣기 불가<br/>`CanCopyPaste: 0`이 설정된 열에서는 `Ctrl + C` 실행 시 빈 셀이 복사되며 `Ctrl + V`는 무시됩니다.<br/>영역을 복사하여 붙여넣을 때 `CanCopyPaste: 0` 열이 포함된 경우 해당 열 이후의 데이터는 붙여넣기 되지 않습니다.<br/>시트 내에서 드래그로 영역을 복사할 경우 해당 열은 없는 것처럼 건너뛰어 클립보드에 복사됩니다.|
|`1(true)`|복사/붙여넣기 가능 (`default`)|


### Example
```javascript
// 특정 열의 복사/붙여넣기 제한
options.Cols = [
    {Type: "Int", Name: "Rank_Sales", CanCopyPaste: false}
];
```

### Read More
- [CopyCols cfg](/docs/props/cfg/copy-cols)
- [PasteCols cfg](/docs/props/cfg/paste-cols)
- [PasteFocused cfg](/docs/props/cfg/paste-focused)
- [SelectingCells cfg](/docs/props/cfg/selecting-cells)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
