# FilterEnumKeys ***(filter cell)***

<!-- synonyms: FilterEnumKeys, filter-enum-keys, Enum 필터, EnumKeys 필터, 코드값 필터, 이넘 키, 이넘 필터, filter enum, enum keys filter, filter by code, Enum 필터링, EnumKeys 필터링 -->

> Enum 타입의 컬럼에서 필터링시 Enum(문자열)이 아닌 EnumKeys(코드값)를 기준으로 필터링 하게 합니다.
>
> 이 속성은 시트 생성 시점에서 Def.Filter를 통해 설정하실 수 있습니다.
> 동일한 Enum 값이 있는 경우, 이 속성을 1로 설정해야 EnumKeys를 기준으로 구분지어 필터링 할 수 있습니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|Enum(문자열) 기준으로 필터 (`default`)|
|`1(true)`|EnumKeys(코드값) 기준으로 필터|


### Example
```javascript
//Enum 타입 컬럼명을 "Nation" 이라고 가정합니다
var option = {
    Def: {
        Filter: {
            Nation: {
                FilterEnumKeys: 1 //Enum컬럼을 Key값을 기준으로 필터링
            }
        }
    }
}
```

### Read More


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
