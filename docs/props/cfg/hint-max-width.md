# HintMaxWidth ***(cfg)***

<!-- synonyms: HintMaxWidth, hint max width, tooltip max width, hint width limit, hint size, 힌트 최대 너비, 힌트 너비, 툴팁 너비 제한, Hint MaxWidth, 힌트 크기 -->

> 힌트의 최대 너비(`px`)를 설정합니다.  
> 힌트 내용이 지정한 너비를 넘으면 지정한 너비에서 줄바꿈되어 표시됩니다.  
> 열 단위로 설정하려면 [HintMaxWidth col](/docs/props/col/hint-max-width)을 사용합니다. 둘 다 설정된 경우 `Cfg` 설정이 우선 적용됩니다.

### Type
`number`

### Options

|Value|Description|
|-----|-----|
|`number`|힌트의 최대 너비 (`px`)|

### Example
```javascript
options.Cfg = {
    HintMaxWidth: 500 // 힌트의 최대 너비를 500px로 설정
};
```

### Read More
- [HintMaxWidth col](/docs/props/col/hint-max-width)
- [HintMaxHeight cfg](./hint-max-height)
- [ShowHint row](/docs/props/row/show-hint)
- [ShowHint col](/docs/props/col/show-hint)
- [ShowHint cell](/docs/props/cell/show-hint)

### Since

|product|version|desc|
|---|---|---|
|core|8.3.0.47|기능 추가|
