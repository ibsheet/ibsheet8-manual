# DecimalAdjust ***(cfg)***

> `Int`, `Float` 타입 컬럼의 근사값 처리 방식을 설정합니다.  
> `Int` 타입은 소수점이 포함된 값이 조회되는 경우,  
> `Float` 타입은 `Format`에 지정한 자릿수를 초과하는 값이 조회되는 경우 적용됩니다.  
> `DecimalAdjust`는 `Cfg`, `Col`, `Cell`에 설정할 수 있으며,  
> 적용 우선순위는 `Cell` > `Col` > `Cfg` 입니다.

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
options = {
  Cfg: {
    DecimalAdjust: "ceil" // 전역 기본값
  },
  Cols: [
    { Header: "정수", Type: "Int", Name: "sInt" }, // Cfg(ceil) 적용
    { Header: "실수(내림)", Type: "Float", Name: "nFloat_floor", Format: "#,##0.###", DecimalAdjust: "floor" }, // Col이 Cfg를 덮어씀
    { Header: "실수(반올림)", Type: "Float", Name: "nFloat_round", Format: "#,##0.###", DecimalAdjust: "round" } // Col이 Cfg를 덮어씀
  ]
};
```

### Try it
- [Demo of DecimalAdjust](https://jsfiddle.net/gh/get/library/pure/ibsheet/ibsheet8-manual-sample/tree/master/samples/properties/Cfg/DecimalAdjust-round/)


### Read More

- [DecimalAdjust col](/docs/props/col/decimal-adjust)
- [DecimalAdjust cell](/docs/props/cell/decimal-adjust)
- [Format appendix](/docs/appx/format)
 
### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.11|기능 추가|
