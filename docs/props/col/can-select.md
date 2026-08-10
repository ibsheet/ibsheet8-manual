# CanSelect ***(col)***

<!-- synonyms: 선택 가능, 열 선택, 범위 선택, 선택 제외, 드래그 선택 제외, selectable, column select, range select exclude, drag select -->

> 해당 열의 선택 가능 여부를 설정합니다.  
> 드래그를 통한 범위 선택 시 `CanSelect: 0`으로 설정된 열은 선택 범위에 포함되지 않습니다.

![canSelect](/assets/imgs/canSelect.png "드래그하여 선택시 선택 가능여부")
> 위 예시에서 `CanSelect: 0`으로 설정된 열은 선택되지 않으며,
> 범위 복사 시에도 해당 열은 제외됩니다.


### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|해당 열 선택 불가|
|`1(true)`|해당 열 선택 가능 (`default`)|

### Example
```javascript
// AMT 열을 선택 범위에서 제외
options.Cols = [
    {Type: "Int", Name: "AMT", CanSelect: 0, Width: 120}
];
```

### Read More
- [CanSelect cfg](/docs/props/cfg/can-select)
- [CanSelect row](/docs/props/row/can-select)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
