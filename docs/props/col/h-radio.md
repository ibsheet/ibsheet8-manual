# HRadio ***(col)***

<!-- synonyms: 라디오 단일 선택, 한 열에 하나만, 한 행에 하나만, 컬럼 단일 체크, 행 단일 체크, Radio 그룹, horizontal radio -->

> `Type`이 `Radio`인 열에서 단일 선택의 방향(열 단위 / 행 단위)을 설정합니다.  
> `0(false)`: 한 열에서 한 셀만, `1(true)`: 한 행에서 한 셀만 선택 가능합니다.  
> 명시적인 default 값이 없으므로 필요한 방향을 직접 지정해야 합니다.

### Type
`boolean`

### Options
|Value|동작|예시 이미지|
|-----|-----|-----|
|`0(false)` | 한 **열** 안에서 하나의 셀만 선택 가능|![HRadio 0](/assets/imgs/hradio0.png "HRadio:0")|
|`1(true)` | 한 **행** 안에서 하나의 셀만 선택 가능|![HRadio 1](/assets/imgs/hradio1.png "HRadio:1")|


### Example
```javascript
options.Cols = [
    // 컬럼 내 단일 선택: st1 컬럼 안에서 한 셀만 체크 가능
    {Type: "Radio", Name: "st1", HRadio: 0, ...},

    // 행 내 단일 선택: st2, st3 중 한 셀만 체크 가능
    {Type: "Radio", Name: "st2", HRadio: 1, ...},
    {Type: "Radio", Name: "st3", HRadio: 1, ...}
];
```

### Read More
- [Radio col](./radio)
- [Range col](./range)
- [Enum col](./enum)
- [EnumKeys col](./enum-keys)
- [RadioIcon col](./radio-icon)
- [RadioIconWidth col](./radion-icon-width)
- [BoolGroup col](./bool-group)
- [Type appendix](/docs/appx/type)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
