# Pos ***(col)***

<!-- synonyms: 열 위치, 컬럼 인덱스, 섹션 내 위치, 열 순서, position, column index, column position, section position -->

> 섹션 내에서 열의 인덱스를 확인합니다.
>
> 시트의 열 생성시, `LeftCols` 배열에 추가한 열은 틀고정을 기준으로 좌측 섹션으로 들어가고, `Cols` 배열에 넣은 열은 가운데, `RightCols` 섹션에 넣은 열은 우측 섹션으로 추가됩니다.
>
> 이 속성은 자신의 섹션 내에서 왼쪽을 기준으로 몇번째로 열이 위치하고 있는지를 확인합니다. (`Readonly`)

###
![섹션](/assets/imgs/section.png "섹션")<br/>

### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`number`|섹션 내에 순번(좌측 기준 0부터 시작)<br>`LeftCols`에는 제품 내부적으로 사용하는 숨겨진 열이 있어 1부터 시작합니다.<br>또한 `SEQ` 열을 별도로 지정하지 않는 경우, 자동으로 `LeftCols`에 `SEQ` 열이 감춰진 상태로 생성됩니다.|



### Example
```javascript
//열의 순번을 확인
var pos = sheet.getAttribute({col: "RENTFEE", attr: "Pos"})
```

### Read More
- [Section col](./section)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
