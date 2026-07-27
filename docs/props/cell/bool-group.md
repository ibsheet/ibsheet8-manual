# BoolGroup ***(cell)***

<!-- synonyms: 라디오 그룹, 단일 체크, 그룹 체크, 하나만 체크, bool radio cell -->

> `Bool` 타입 컬럼에서 특정 셀들을 같은 그룹으로 묶어, 그 그룹 안에서 한 셀만 체크되도록 합니다.  
> 같은 그룹 인덱스를 가진 셀끼리 라디오처럼 묶이며, 체크 시 같은 그룹의 다른 셀은 자동 체크해제됩니다.  
> 컬럼 단위로 그룹을 묶으려면 [BoolGroup col](/docs/props/col/bool-group)을 사용하세요.

###
![BoolGroup](/assets/imgs/boolGroup.png "그룹으로 묶인 행에서 하나만 선택 가능")

### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`number` | 라디오처럼 하나로 묶을 그룹 인덱스|

### Example
```javascript
// AR1~AR3은 1번 그룹, AR4~AR6은 2번 그룹 — 각 그룹 안에서 한 셀만 체크 가능
sheet.setAttribute(sheet.getRowById("AR1"), "CLS", "BoolGroup", "1");
sheet.setAttribute(sheet.getRowById("AR2"), "CLS", "BoolGroup", "1");
sheet.setAttribute(sheet.getRowById("AR3"), "CLS", "BoolGroup", "1");
sheet.setAttribute(sheet.getRowById("AR4"), "CLS", "BoolGroup", "2");
sheet.setAttribute(sheet.getRowById("AR5"), "CLS", "BoolGroup", "2");
sheet.setAttribute(sheet.getRowById("AR6"), "CLS", "BoolGroup", "2");
```

### Read More
- [BoolGroup col](/docs/props/col/bool-group)
- [Radio cell](/docs/props/cell/radio)
- [BoolIcon cell](/docs/props/cell/bool-icon)
- [Type appendix](/docs/appx/type)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
