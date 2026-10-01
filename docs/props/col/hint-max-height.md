# HintMaxHeight ***(col)***

<!-- synonyms: HintMaxHeight, hint max height, tooltip max height, hint height limit, hint scroll, 힌트 최대 높이, 힌트 높이, 툴팁 높이 제한, 힌트 스크롤, 긴 힌트, 열 힌트 높이 -->

> 해당 열에 표시되는 힌트의 최대 높이(`px`)를 설정합니다.  
> 힌트 내용이 지정한 높이를 넘으면 힌트 안에 세로 스크롤이 생기며, 마우스가 힌트 위에 있는 동안에는 힌트가 닫히지 않아 스크롤해서 내용을 확인할 수 있습니다.  
> 화면에 표시할 수 있는 공간이 지정한 높이보다 작으면 화면 안에 들어가는 높이까지만 표시됩니다.  
> [HintMaxHeight cfg](/docs/props/cfg/hint-max-height)가 설정되어 있으면 `Cfg` 설정이 우선 적용됩니다.

### Type
`number`

### Options

|Value|Description|
|-----|-----|
|`number`|힌트의 최대 높이 (`px`)|

### Example
```javascript
options.Cols = [
    // 메모 열의 힌트는 최대 150px 높이로 표시, 넘는 내용은 스크롤로 표시
    {Type: "Text", Name: "Memo", Width: 120, ShowHint: 1, HintMaxHeight: 150}
];
```

### Read More
- [HintMaxHeight cfg](/docs/props/cfg/hint-max-height)
- [HintMaxWidth col](./hint-max-width)
- [ShowHint col](./show-hint)

### Since

|product|version|desc|
|---|---|---|
|core|8.4.0.20|기능 추가|
