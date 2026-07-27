# Spanned ***(row)***

> 행 내에서 좌우 열간에 병합을 허용할지 여부를 설정합니다.  
> `Def.Row`나 `Def.Header`에서 설정하면 헤더 영역이나 데이터 영역에서 [Span](/docs/props/cell/span) 속성을 통해 좌우 셀을 병합할 수 있습니다.  
> 자동 머지([DataMerge](/docs/props/cfg/data-merge))와는 별도로 동작하므로 자동 머지를 꺼야 합니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|Span(좌우병합) 허용하지 않음 (`default`)|
|`1(true)`|Span(좌우병합) 허용|


### Example
![Spanned](/assets/imgs/headerMerge.png "Spanned")
```javascript
//헤더 행에 대해 좌우로 병합
options.Def.Header = {Spanned:true};
options.Cfg = {
    DataMerge: 0,  // 자동머지 끔
    HeaderMerge: 0
};
options.Cols = [
    {Header:[{Value:"(행사)매출실적",Span:4,Align:"Center"},{Value:"1월"}],Name:"Col1"},
    {Header:[{},{Value:"2월"}],Name:"Col2"},
    {Header:[{},{Value:"3월"}],Name:"Col3"},
    {Header:[{},{Value:"4월"}],Name:"Col4"},
];
```

### Read More
- [Spanned col](/docs/props/col/spanned)
- [Span cell](/docs/props/cell/span)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
