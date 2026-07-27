# SpinnerField ***(col)***

<!-- synonyms: 스피너 단위, 날짜 스피너 단위, 증감 단위, date spinner unit, year month day hour minute second -->

> [Type](/docs/appx/type)이 `Date`이고 [SpinnerVisible](./spinner-visible)을 사용하는 열에서 스피너 화살표 클릭 시 증감되는 단위를 설정합니다.
>
> `y`(년), `M`(월), `d`(일), `H`(시), `m`(분), `s`(초) 중 하나를 지정합니다.
>
> 설정하지 않으면 `d`(일)가 기본값으로 적용됩니다. 대소문자에 유의하세요 — 월은 대문자 `M`, 분은 소문자 `m`입니다.

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
    // 주문일자 — 월 단위로 스피너 증감
    {Type: "Date", Name: "OrderDate", SpinnerVisible: true, SpinnerField: "M", Format: "yyyy-MM-dd"},

    // 출고시각 — 분 단위로 스피너 증감
    {Type: "Date", Name: "ShipTime", SpinnerVisible: true, SpinnerField: "m", Format: "yyyy-MM-dd HH:mm:ss"},
    ...
];
```

### Read More
- [Type appendix](/docs/appx/type)
- [SpinnerVisible col](./spinner-visible)
- [SpinnerField cell](/docs/props/cell/spinner-field)
- [Format col](./format)

### Since

|product|version|desc|
|---|---|---|
|core|8.4.0.4|기능 추가|
