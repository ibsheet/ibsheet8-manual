# DecimalAdjust ***(cell)***

<!-- synonyms: 소수점 처리, 반올림, 올림, 내림, 근사값 처리, 자릿수 조정, 소수점 반올림, round, floor, ceil, decimal-adjust, decimal adjust, decimal rounding, float rounding, int decimal -->

> `Int`, `Float` 타입 컬럼의 근사값 처리 방식을 설정합니다.  
> `Int` 타입은 소수점이 포함된 값이 조회되는 경우 적용됩니다.  
> `Float` 타입은 `Format`에 지정한 자릿수를 초과하는 값이 조회되는 경우 적용됩니다.

### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`round`|반올림 처리 (`default`)|
|`floor`|내림 처리|
|`ceil`|올림 처리|

```javascript
// 조회 데이터에서 특정 셀에만 속성 적용 (컬럼명: FloatData)
{
  data: [
    {
      FloatData: 15.1,
      FloatDataDecimalAdjust: "floor" // 해당 셀의 근사값 처리 방식을 내림으로 설정
    }
  ]
}
```
### Try it
- [Demo of DecimalAdjust](https://jsfiddle.net/gh/get/library/pure/ibsheet/ibsheet8-manual-sample/tree/master/samples/properties/Cfg/DecimalAdjust-round/)


### Read More

- [DecimalAdjust cfg](/docs/props/cfg/decimal-adjust)
- [DecimalAdjust col](/docs/props/col/decimal-adjust)
- [Format appendix](/docs/appx/format)
- 
### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.11|기능 추가|
