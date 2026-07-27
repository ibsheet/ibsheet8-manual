# DecimalAdjust ***(col)***

> `Int`, `Float` 타입 컬럼의 근사값 처리 방식을 설정합니다.  
> `Int` 타입은 소수점이 포함된 값이 조회되는 경우 적용됩니다.  
> `Float` 타입은 `Format`에 지정한 자릿수를 초과하는 값이 조회되는 경우 적용됩니다.  
> `Cell`에 동일 속성이 설정된 경우 `Cell` 설정이 우선 적용됩니다.

### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`round`|반올림 처리 (`default`)|
|`floor`|내림 처리|
|`ceil`|올림 처리|

### Example
```javascript
options.Cols = [
  {
    Header: "금액",
    Type: "Float",
    Name: "amount",
    Format: "#,##0.###",
    DecimalAdjust: "floor" // 해당 컬럼의 근사값 처리 방식을 내림으로 설정
  }
];
```
### Try it
- [Demo of DecimalAdjust](https://jsfiddle.net/gh/get/library/pure/ibsheet/ibsheet8-manual-sample/tree/master/samples/properties/Cfg/DecimalAdjust-round/)


### Read More

- [DecimalAdjust cfg](/docs/props/cfg/decimal-adjust)
- [DecimalAdjust cell](/docs/props/cell/decimal-adjust)
- [Format appendix](/docs/appx/format) 

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.11|기능 추가|
