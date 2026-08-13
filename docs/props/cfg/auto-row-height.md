# AutoRowHeight ***(cfg)***

<!-- synonyms: auto row height, dynamic row height, variable row height, row height auto adjust, 가변 행 높이, 행 높이 자동, 줄바꿈 행 높이 -->

> [SearchMode](/docs/props/cfg/search-mode): 0, 3 시트에서, 데이터 행의 높이가 서로 달라도 **세로 스크롤과 화면 렌더링이 정확**하도록 지원하는 옵션입니다.  
> 이미지나 여러 줄 텍스트로 인해 행 높이가 달라지는 경우에도, 각 행의 높이에 맞춰 스크롤과 화면 표시를 정확히 처리합니다.


### 적용 가능한 컬럼 조건
`AutoRowHeight`는 아래 조건을 만족하는 컬럼이 하나 이상 존재할 경우에만 적용됩니다.

- 컬럼 타입: `Lines`, `Html`, `Img`, `Button`
- 컬럼 속성:
  - [Wrap](/docs/props/col/wrap)
  - [HtmlPrefix](/docs/props/col/html-prefix)
  - [HtmlPostfix](/docs/props/col/html-postfix)
  - [TextSize](/docs/props/col/text-size)

### 제약사항
- `AutoRowHeight`는 **시트 생성 시에만 적용**되며,
   생성 이후 값을 변경해도 동작은 바뀌지 않습니다.
- 적용 가능한 컬럼 조건을 만족하지 않으면,
   `AutoRowHeight: true`로 설정해도 **내부적으로 `false`로 처리됩니다.**
- `SearchMode`가 `0`, `3`일 때 지원됩니다.
- 가변 행 높이를 계산하기 때문에, 데이터가 많거나 행 높이 변화가 큰 경우
  기본 모드보다 스크롤 및 렌더링 성능에 영향을 줄 수 있습니다.


### Type
`boolean`


### Options
|Value|Description|
|-----|-----|
|`0` (`false`)|행 높이 자동 맞춤 사용 안 함 (`default`)|
|`1` (`true`)|행 높이 자동 맞춤 사용|

### Example
```javascript
options = {
  Cfg :{
   SearchMode: 0,
   //데이터행의 높이를 계산
   AutoRowHeight: true
  }
};
```

### Try it
- [Demo of AutoRowHeight](https://jsfiddle.net/gh/get/library/pure/ibsheet/ibsheet8-manual-sample/tree/master/samples/properties/Cfg/AutoRowHeight-true/)

### Read More
- [SearchMode cfg](/docs/props/cfg/search-mode)
- [Wrap col](/docs/props/col/wrap)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.27|기능 추가|
|core|8.3.0.19|`SignFontStyle`속성 중 `TextSize` 대응 추가|