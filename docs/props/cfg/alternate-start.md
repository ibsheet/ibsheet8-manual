# AlternateStart ***(cfg)***
> `Alternate`로 지정된 반복 구간 내에서 배경색이 적용될 **첫 번째 행 위치**를 지정하는 옵션입니다. 
> - 값 `0`은 간격의 **첫 번째 행**부터 시작함을 의미합니다.  

### 동작 요약
- 반복 구간에서 색을 적용할 **시작 행을 지정**합니다.
- 기본값은 `(cfg)Alternate - (cfg)AlternateCount`이며,  
  시작 위치는 `AlternateCount`와 함께 반복 구간 내에서 색 적용 위치를 결정합니다.

### 이미지 예시
![AlternateStart](/assets/imgs/alternateStart.png "AlternateStart")
> 예시: `Alternate: 5`, `AlternateCount: 2`, `AlternateStart: 0`  
> 5행 반복 구간에서 **맨 위 2개의 행**에 색이 적용됩니다.

![AlternateStart](/assets/imgs/alternateCount.png "AlternateStart")
> 예시 : `Alternate: 5`, `AlternateCount: 2`  
> 5행 반복 구간에서 **마지막 2개의 행**에 색이 적용됩니다.



### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`number`|반복 구간 내에서 색이 적용될 시작 행 위치(`default :  (cfg)Alternate - (cfg)AlternateCount`)|


### Example
```javascript
options = {
    Cfg:{
     Alternate: 5,        // 5행마다 반복
     AlternateCount: 2,   // 반복 구간에서 마지막 2행만 색칠
     AlternateStart: 0    // 반복 구간의 맨 위부터 색칠 시작

    }
};
```

### Read More
- [Alternate cfg](./alternate)
- [AlternateColor row](/docs/props/row/alternate-color)
- [AlternateClass row](/docs/props/row/alternate-class)
- [AlternateCount cfg](./alternate-count)
- [AlternateType cfg](./alternate-type)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
