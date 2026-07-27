# Radio ***(col)***

<!-- synonyms: 라디오 그룹, 행 단일 선택, 그룹 인덱스, 컬럼 묶기, radio group -->

> `Type`이 `Bool` 또는 `Radio`인 열들을 그룹으로 묶어, 한 행 내 같은 그룹의 컬럼들 중 한 셀만 체크 가능하게 합니다.  
> 같은 숫자(그룹 인덱스)를 부여한 컬럼들이 하나의 그룹이 되며, 그룹별로 별도의 단일 선택 동작이 이루어집니다.

###
![Radio](/assets/imgs/radio.png "같은 행에서 같은 그룹 내 하나만 선택 가능")

### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`number` | 라디오처럼 하나로 묶을 그룹 인덱스|

### Example
```javascript
options.Cols = [
    // 1번 그룹: st1~st5 중 한 셀만 선택 가능
    {Type: "Bool", Name: "st1", Radio: 1, ...},
    {Type: "Bool", Name: "st2", Radio: 1, ...},
    {Type: "Bool", Name: "st3", Radio: 1, ...},
    {Type: "Bool", Name: "st4", Radio: 1, ...},
    {Type: "Bool", Name: "st5", Radio: 1, ...},
    // 2번 그룹: att1~att5 중 한 셀만 선택 가능
    {Type: "Bool", Name: "att1", Radio: 2, ...},
    {Type: "Bool", Name: "att2", Radio: 2, ...},
    {Type: "Bool", Name: "att3", Radio: 2, ...},
    {Type: "Bool", Name: "att4", Radio: 2, ...},
    {Type: "Bool", Name: "att5", Radio: 2, ...}
];
```

### Read More
- [BoolGroup col](./bool-group)
- [Range col](./range)
- [Enum col](./enum)
- [EnumKeys col](./enum-keys)
- [Type appendix](/docs/appx/type)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
