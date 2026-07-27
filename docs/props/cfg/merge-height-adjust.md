# MergeHeightAdjust ***(cfg)***

> [HtmlPrefix](/docs/props/col/html-prefix)나 [HtmlPostfix](/docs/props/col/html-postfix)와 같이 셀의 높이에 영향을 주는 기능 사용 시, 병합 영역의 레이아웃 깨짐이 발생하면 높이를 보정합니다.  
> `true`로 설정 시 병합 정보를 확인하여 수행되므로, 병합이 많은 경우 성능이 저하될 수 있습니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|병합된 행의 높이 보정 안함 (`default`)|
|`1(true)`|병합된 행의 높이 보정|

### Example
```javascript
options.Cfg = {
  MergeHeightAdjust: 1 // 병합된 영역의 높이 보정
};
```

### Read More
- [HtmlPrefix row](/docs/props/row/html-prefix)
- [HtmlPrefix col](/docs/props/col/html-prefix)
- [HtmlPrefix cell](/docs/props/cell/html-prefix)
- [HtmlPostfix row](/docs/props/row/html-postfix)
- [HtmlPostfix col](/docs/props/col/html-postfix)
- [HtmlPostfix cell](/docs/props/cell/html-postfix)

### Since

|product|version|desc|
|---|---|---|
|core|8.3.0.3|기능 추가|
