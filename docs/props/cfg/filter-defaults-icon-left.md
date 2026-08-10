# FilterDefaultsIconLeft ***(cfg)***

<!-- synonyms: FilterDefaultsIconLeft, filter defaults icon left, filter checkbox left, defaults filter icon, filter icon position, 필터 체크박스 왼쪽, 필터 아이콘 왼쪽, Defaults 필터 아이콘, 필터 메뉴 아이콘 위치, 체크박스 좌측 정렬 -->

> 필터 행에서 [Defaults](/docs/props/col/defaults) 를 사용할 때 필터링 시 생성되는 필터 메뉴의 체크 박스 아이콘을 왼쪽에 위치시킬지 여부를 설정합니다

### Type
`boolean`


### Options

|Value|Description|
|-----|-----|
|`0(false)`|필터 체크 박스를 오른쪽에 위치 (`default`)|
|`1(true)`|필터 체크 박스를 왼쪽에 위치|


### Example
```javascript
options.Cfg = {
    FilterDefaultsIconLeft: true
};
```

### Read More
 - [Defaults col](/docs/props/col/defaults)
 - [FilterEnumIconLeft cfg](./filter-enum-icon-left)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.7|기능 추가|
