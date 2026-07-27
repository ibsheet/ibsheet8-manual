# Spanned ***(col)***
> 특정 열에 속한 셀들에 대해서 위/아래로 병합할지 여부를 설정합니다.  
> 실제 병합은 [RowSpan](/docs/props/cell/row-span) 속성을 사용합니다.  
> 자동 머지([DataMerge](/docs/props/cfg/data-merge))와는 별도로 동작하므로 자동 머지를 꺼야 합니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|병합 불가 (`default`)|
|`1(true)`|병합 가능|

### Example
```javascript
//전체 열들에 대해서 상/하 병합을 허용
options.Def.Col = {Spanned: true};
options.Cfg = {
    DataMerge: 0,  // 자동머지 끔
    HeaderMerge: 0
};
// 헤더행을 위아래로 병합
options.Cols = [
    {
        Header: [
            {Value: "매장명", RowSpan: 2, Align: "Center"}, // 1행: 아래로 2칸 병합
            {}                                               // 2행: 병합되어 표시 안됨
        ],
        Type: "Text",
        Name: "storeName"
    }
];
```

### Read More
- [RowSpan cell](/docs/props/cell/row-span)
- [Spanned row](/docs/props/row/spanned)
- [DataMerge cfg](/docs/props/cfg/data-merge)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
