# Alternate ***(cfg)***
> 홀수, 짝수 행에 대해 번갈아 배경색을 설정하여 가독성을 높이는 기능입니다.
> 기본 배경색은 CSS 파일의 `.IBColorAlternate` 색상을 사용합니다.  
> (Row)[AlternateColor](/docs/props/row/alternate-color)를 설정하면 해당 색상이 적용됩니다.
> 옵션 값이 `3` 이상인 경우 (cfg)[AlternateStart](./alternate-start)와 (cfg)[AlternateCount](./alternate-count)에 따라 색 적용 방식이 조정됩니다.


### 옵션별 동작 이미지
![Alternate0](/assets/imgs/alternate0.png "Alternate0")
> 예시: `Alternate: 0` → 배경색 교차 기능 사용 안함
>
![Alternate2](/assets/imgs/alternate2.png "Alternate0")
> 예시: `Alternate: 2` → 홀수/짝수 행에 배경색 적용

### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`0`|배경색 교차 기능 사용 안함 (CSS 파일의 `.IBColorDefault` 색상, `default`)|
|`1`|모든 데이터 행에 배경색 적용 (CSS 파일의 `.IBColorAlternate` 색상)|
|`2`|짝수 행에 배경색 적용 (CSS 파일의 `.IBColorDefault`, `.IBColorAlternate` 색상이 반복적으로 표시)|
|`3`|3개 행마다 마지막 행에 배경색 적용|
|`N`|N개 행마다 마지막 행에 배경색 적용|


### Example
```javascript

//1. 홀수/짝수 행에 배경색 적용(main.css정의된 색상으로 홀수/짝수 배경색 적용)
options = {
    Cfg:{
      Alternate: 2, 
    }
 };

// 2. 짝수번째 배경색을 노란색으로 변경하려면 AlternateColor 사용
options = {
    Cfg:{
      Alternate: 2, 
    },
    Def:{
      Row:{
          AlternateColor: "FFFF00" // 짝수번째 행에 적용될 색상
      }
    }
 }
```

### Read More
- [AlternateColor row](/docs/props/row/alternate-color)
- [AlternateClass row](/docs/props/row/alternate-class)
- [AlternateCount cfg](./alternate-count)
- [AlternateStart cfg](./alternate-start)
- [AlternateType cfg](./alternate-type)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
