# HintMaxWidth ***(col)***

<!-- synonyms: HintMaxWidth, hint max width, tooltip max width, hint width limit, 힌트 최대 너비, 힌트 너비, 툴팁 너비 제한, 열 힌트 너비, 힌트 줄바꿈 -->

> 해당 열에 표시되는 힌트의 최대 너비(`px`)를 설정합니다.  
> 힌트 내용이 지정한 너비를 넘으면 지정한 너비에서 줄바꿈되어 표시됩니다.  
> [HintMaxWidth cfg](/docs/props/cfg/hint-max-width)가 설정되어 있으면 `Cfg` 설정이 우선 적용됩니다.

### Type
`number`

### Options

|Value|Description|
|-----|-----|
|`number`|힌트의 최대 너비 (`px`)|

### Example
```javascript
options.Cols = [
    // 메모 열의 힌트는 최대 300px 너비로 표시, 넘는 내용은 줄바꿈
    {Type: "Text", Name: "Memo", Width: 120, ShowHint: 1, HintMaxWidth: 300}
];
```

### Read More
- [HintMaxWidth cfg](/docs/props/cfg/hint-max-width)
- [HintMaxHeight col](./hint-max-height)
- [ShowHint col](./show-hint)

### Since

|product|version|desc|
|---|---|---|
|core|8.3.0.47|기능 추가|
