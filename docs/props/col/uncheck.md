# Uncheck ***(col)***

<!-- synonyms: 체크해제 허용, 라디오 체크해제, 그룹 체크해제, bool 토글, uncheck -->

> `Type:"Bool"` 열에서 [Radio](./radio)나 [BoolGroup](./bool-group)으로 단일 선택을 적용한 경우, 이미 체크된 셀을 다시 클릭했을 때 체크해제를 허용할지 여부를 설정합니다.

###
![Radio](/assets/imgs/radio.png "같은 행에서 하나만 선택 가능")

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)` | 체크해제 허용 안 함|
|`1(true)` | 체크해제 허용 (`default`)|

### Example
```javascript
options.Cols = [
    // Radio 그룹에서 한 번 체크되면 체크해제 불가
    {Type: "Bool", Name: "st1", Radio: 1, Uncheck: 0, ...},
    {Type: "Bool", Name: "st2", Radio: 1, Uncheck: 0, ...},
    {Type: "Bool", Name: "st3", Radio: 1, Uncheck: 0, ...}
];
```

### Read More
- [Uncheck cell](/docs/props/cell/uncheck)
- [Radio col](./radio)
- [BoolGroup col](./bool-group)
- [RadioUncheck col](./radio-uncheck)
- [Type appendix](/docs/appx/type)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
