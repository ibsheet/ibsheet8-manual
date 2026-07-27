# AlternateType ***(cfg)***

> 트리로 구성된 시트에서 자식행들도 [Alternate](./alternate) 계산에 포함될지 여부를 설정합니다.


### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`0`|트리 시트의 자식행을 포함하지 않고 하이라이트 표시.(`default`)|
|`1`|트리 시트의 모든 자식행을 포함하여 Alternate 계산 및 색칠.<br/>트리를 접거나 펼쳐도 계산 방식은 동일하게 유지됩니다.<br/>**주의:** 행이 많거나 트리를 자주 펼치고 접으면 시트가 느려질 수 있습니다. |


### Example
```javascript
options = {
  Cfg :{
    Alternate: 2,        // 짝수행에 하이라이트 표시
    AlternateType: 1     // 트리시트에서 자식행도 Alternate 에 포함하여 하이라이트 처리
  }
};
```

### Read More
- [Alternate cfg](./alternate)
- [AlternateColor row](/docs/props/row/alternate-color)
- [AlternateClass row](/docs/props/row/alternate-class)
- [AlternateCount cfg](./alternate-count)
- [AlternateStart cfg](./alternate-start)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
