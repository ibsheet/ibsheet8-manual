# BoolGroup ***(col)***

<!-- synonyms: 라디오 그룹, 단일 체크, 그룹 체크, 하나만 체크, bool radio -->

> `Bool` 타입 컬럼을 라디오처럼 동작시켜 컬럼 안에서 한 셀만 체크되도록 합니다.  
> 특정 셀들끼리만 그룹으로 묶으려면 [BoolGroup cell](/docs/props/cell/bool-group)을 사용하세요.

### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`number` | 라디오처럼 하나로 묶을 그룹 인덱스|

### Example
```javascript
options.Cols = [
    // 해당 컬럼 안에서 한 셀만 체크 가능
    {Type: "Bool", Name: "st1", BoolGroup: 1, ...}
];
```

### Read More
- [BoolGroup cell](/docs/props/cell/bool-group)
- [Radio col](./radio)
- [Uncheck col](./uncheck)
- [Type appendix](/docs/appx/type)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
