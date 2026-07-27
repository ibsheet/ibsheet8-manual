# AlternateCount ***(cfg)***
> `Alternate`로 지정된 반복 구간 내에서 **배경색이 적용될 마지막 행의 개수**를 지정하는 옵션입니다.  
> 행 단위로 반복되는 배경색 패턴을 만들 때 사용됩니다.

### 동작 요약
- 각 반복 구간에서 `AlternateCount`로 지정한 행 수만큼 배경색이 적용됩니다.
- 기본적으로 반복 구간의 마지막 행들에 색이 적용되며, 시작 위치는 `AlternateStart` 설정에 따라 달라질 수 있습니다.

### 이미지 예시
![AlternateCount](/assets/imgs/alternateCount.png "AlternateCount")
> 예시 : `Alternate: 5`, `AlternateCount: 2`  
> 5행 반복 구간에서 **마지막 2개의 행**에 색이 적용됩니다.



### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`number`|반복 구간 내에서 배경색이 적용될 행의 개수 (`default: 1`)|


### Example
```javascript
options = {
  Cfg: {
    Alternate:5,     // 5행마다 반복
    AlternateCount:2  // 각 구간에서 2개의 행에 색 적용
  }
```

### Read More

- [Alternate cfg](./alternate)
- [AlternateColor row](/docs/props/row/alternate-color)
- [AlternateClass row](/docs/props/row/alternate-class)
- [AlternateStart cfg](./alternate-start)
- [AlternateType cfg](./alternate-type)


### Since
|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
