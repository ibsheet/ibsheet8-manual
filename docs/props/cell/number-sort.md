# NumberSort ***(cell)***

<!-- synonyms: NumberSort, number-sort, 숫자 정렬, 숫자 소팅, 숫자형 정렬, 문자 정렬, 정렬 방식, 소팅 타입, 숫자 기준 정렬, number sort, numeric sort, sort as number, sort mode -->

> 셀의 데이터를 숫자형식으로 소팅할지 여부를 설정합니다.
>
> 일반적으로 `Int, Float, Date Type`은 숫자형식으로, 그 외의 [Type](/docs/appx/type)은 문자형식으로 소팅이 이루어집니다.
>
> 여기서 값을 `0(false)`으로 설정하면, Type과 무관하게 문자형식으로 소팅되고, `1(true)`로 설정시 숫자형식으로 소팅이 이루어집니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|문자형식의 소팅|
|`1(true)`|숫자형식의 소팅|


### Example
```javascript
//조회 데이터 내에서 속성 적용  (열이름: CLS)
//특정 셀에 대해 숫자형식으로 소팅
{
    data:[
        {... , "CLSNumberSort":"1" , ...}
    ]
}
```

### Read More
- [RawSort cell](./raw-sort)
- [SortValue cell](./sort-value)
- [CaseSensitive cell](./case-sensitive)
- [Type appendix](/docs/appx/type)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
