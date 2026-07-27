# Span ***(cell)***
> 특정 셀을 기준으로 오른쪽으로 합쳐질 셀의 개수를 설정합니다.  
> `row`에 [Spanned](/docs/props/row/spanned):`1`이 설정되어 있어야 사용할 수 있습니다.  
> [DataMerge](/docs/props/cfg/data-merge), [HeaderMerge](/docs/props/cfg/header-merge) 설정 시 적용되지 않습니다.  
> [setMergeRange](/docs/funcs/core/set-merge-range) 사용 시 동적으로 병합할 수 있습니다.



### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`number`|행 내에서 오른쪽으로 합쳐질 셀 개수|



### Example
```javascript
//Spanned가 설정되어 있어야 함.
options.Def.Row = {Spanned: 1};

//조회 데이터 내에서 속성 적용  (열이름: CLS)
{
    data:[
        //오른쪽으로 3개 셀을 병합함
        {... ,CLSSpan: 3 ...}
    ]
}
```

### Read More
- [DataMerge cfg](/docs/props/cfg/data-merge)
- [HeaderMerge cfg](/docs/props/cfg/header-merge)
- [RowSpan cell](./row-span)
- [Spanned row](/docs/props/row/spanned)
- [setMergeRange method](/docs/funcs/core/set-merge-range)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
