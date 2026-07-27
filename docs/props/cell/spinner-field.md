# SpinnerField ***(cell)***

<!-- synonyms: 스피너 단위, 날짜 스피너 단위, 증감 단위, date spinner unit, year month day hour minute second -->

> [Type](/docs/appx/type)이 `Date`이고 [SpinnerVisible](./spinner-visible)을 사용하는 셀에서 스피너 화살표 클릭 시 증감되는 단위를 설정합니다.
>
> `y`(년), `M`(월), `d`(일), `H`(시), `m`(분), `s`(초) 중 하나를 지정합니다.
>
> 셀 단위로 지정한 값이 열 단위 [SpinnerField col](/docs/props/col/spinner-field)보다 우선 적용됩니다. 설정하지 않으면 `d`(일)가 기본값입니다. 대소문자에 유의하세요 — 월은 대문자 `M`, 분은 소문자 `m`입니다.

### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`y`|1년 단위 증감|
|`M`|1개월 단위 증감|
|`d`|1일 단위 증감 (`default`)|
|`H`|1시간 단위 증감|
|`m`|1분 단위 증감|
|`s`|1초 단위 증감|

### Example
```javascript
options.Cols = [
    ...
    {Type: "Date", Name: "OrderDate", SpinnerVisible: true, SpinnerField: "d"},
    ...
];

// 데이터 단위로 특정 행의 셀만 증감 단위를 다르게 지정
var data = [
    {OrderDate: "2026-05-29", OrderDateSpinnerField: "M"}, // 이 행은 월 단위 증감
    {OrderDate: "2026-05-30"}                              // 나머지 행은 열 설정(d) 적용
];
```

### Read More
- [Type appendix](/docs/appx/type)
- [SpinnerVisible cell](./spinner-visible)
- [SpinnerField col](/docs/props/col/spinner-field)

### Since

|product|version|desc|
|---|---|---|
|core|8.4.0.4|기능 추가|
