# DefaultDate ***(col)***

<!-- synonyms: 기본 날짜, 초기 날짜, 빈값 날짜 기본값, Date 기본값, 달력 기본 날짜, default date, initial date, date fallback, blank date default -->

> `Date` 타입 컬럼에서 데이터 값이 빈값일 때 특정 날짜를 선택할 수 있도록 설정합니다. <br/>
> 구분자는 지원하지 않고, [DataFormat](../col/data-format) 의 형태를 따라가도록 지원합니다. 


### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`string`|`Date` 타입 컬럼에서 데이터 값이 빈값인 경우 특정 날짜를 선택할 수 있도록 설정|

### Example
```javascript
//버튼 컬럼에 기본 타이틀 지정
options.Cols = [
    {Header: "상세정보", Type: "Button", Name: "DetailBnt", Button: "Button", DefaultDate: "20260727"},
    ...
];
```


### Read More
- [DataFormat col](./data-format)

### Since

|product|version|desc|
|---|---|---|
|core|8.4.0.6|기능 추가|
