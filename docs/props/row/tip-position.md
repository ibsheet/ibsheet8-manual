# TipPosition ***(row)***

> 풍선도움말 객체의 위치나 크기, 정렬을 설정합니다.

### Type
`object`

### Options
|Value|Description|
|-----|-----|
|`X`|풍선도움말의 X축 가감 위치|
|`Y`|풍선도움말의 Y축 가감 위치|


### Example

```javascript
//마지막 행에 풍선도움말 위치 변경
var row = sheet.getLastVisibleRow();
row["TipPosition"] = {Y:-100};
```

### Read More
- [Tip row](./tip)
- [TipClass row](./tip-class)
### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
