# ShiftHint ***(cfg)***

<!-- synonyms: ShiftHint, shift hint, hint position shift, hint left align, tooltip shift, 힌트 위치 이동, 힌트 좌측 이동, Hint 우측 잘림, 힌트 표시 위치, 툴팁 위치 조정, 힌트 자동 이동 -->

> 힌트가 화면 오른쪽 끝을 넘을 만큼 길 때, 힌트 위치를 왼쪽으로 옮겨 셀 내용을 모두 표시할지 여부를 설정합니다.  
> `false`로 설정하면 힌트 위치를 옮기지 않으므로, 힌트로 보여질 내용의 일부가 잘려서 노출되지 않을 수 있습니다.  
> [HintMaxWidth](/docs/props/cfg/hint-max-width)가 설정되어 있으면 `ShiftHint`는 동작하지 않습니다.


### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|화면 오른쪽 공간이 부족해도 힌트 위치를 옮기지 않고 표시|
|`1(true)`|화면 오른쪽 공간이 부족하면 힌트를 왼쪽으로 옮겨 표시 (`default`)|


### Example
```javascript
options.Cfg = {
    ShiftHint: false  // 공간이 부족해도 힌트 위치를 옮기지 않음
};
```

### Read More
- [ShowHint row](/docs/props/row/show-hint)
- [ShowHint col](/docs/props/col/show-hint)
- [ShowHint cell](/docs/props/cell/show-hint)
- [HintMaxWidth cfg](/docs/props/cfg/hint-max-width)
- [HintMaxWidth col](/docs/props/col/hint-max-width)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
