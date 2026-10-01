# HintMaxHeight ***(cfg)***

<!-- synonyms: HintMaxHeight, hint max height, tooltip max height, hint height limit, hint scroll, 힌트 최대 높이, 힌트 높이, 툴팁 높이 제한, 힌트 스크롤, 긴 힌트 -->

> 힌트의 최대 높이(`px`)를 설정합니다.  
> 힌트 내용이 지정한 높이를 넘으면 힌트 안에 세로 스크롤이 생기며, 마우스가 힌트 위에 있는 동안에는 힌트가 닫히지 않아 스크롤해서 내용을 확인할 수 있습니다.  
> 화면에 표시할 수 있는 공간이 지정한 높이보다 작으면 화면 안에 들어가는 높이까지만 표시됩니다.  
> 열 단위로 설정하려면 [HintMaxHeight col](/docs/props/col/hint-max-height)을 사용합니다. 둘 다 설정된 경우 `Cfg` 설정이 우선 적용됩니다.

### Type
`number`

### Options

|Value|Description|
|-----|-----|
|`number`|힌트의 최대 높이 (`px`)|

### Example
```javascript
options.Cfg = {
    HintMaxHeight: 200 // 힌트의 최대 높이를 200px로 설정, 넘는 내용은 스크롤로 표시
};
```

### Read More
- [HintMaxHeight col](/docs/props/col/hint-max-height)
- [HintMaxWidth cfg](./hint-max-width)
- [ShowHint row](/docs/props/row/show-hint)
- [ShowHint col](/docs/props/col/show-hint)
- [ShowHint cell](/docs/props/cell/show-hint)

### Since

|product|version|desc|
|---|---|---|
|core|8.4.0.20|기능 추가|
