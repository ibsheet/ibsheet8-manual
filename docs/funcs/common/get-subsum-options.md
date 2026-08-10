# getSubSumOptions ***(method)***

<!-- synonyms: get subsum options, subtotal options, subsum settings, makeSubTotal options, get subtotal config, subsum configuration, 소계 옵션, 소계 설정 조회, 소계 옵션 확인, makeSubTotal 옵션, 서브합 옵션, getSubSumOptions 메소드 -->

> [makeSubTotal()](../core/make-sub-total)로 시트에 소계 기능을 사용시, 설정된 옵션을 확인합니다. 

### Syntax
```javascript
object getSubSumOptions();
```

### Return Value
***array[option]*** makeSubTotal()에 설정된 옵션
```
[
  {
    "stdCol": 3,
    "avgCols": "B|C",
    "captionCol": [
      {
        "col": "sUnit",
        "val": "%s: %col"
      }
    ],
    "position": "bottom",
    "color": "#dbe2eb",
    "stdColName": "sUnit"
  },
  {
    "stdCol": 2,
    "sumCols": "B|C",
    "position": "bottom",
    "color": "#b2c4d9",
    "stdColName": "sPolicy",
    "captionCol": [
      {
        "col": "sPolicy",
        "val": "%s : %col",
        "cumVal": "%s : %col"
      }
    ]
  }
]
```

### Example
```javascript
// 소계에 설정된 옵션을 배열 형태로 반환합니다.
var opt = sheet.getSubSumOptions();
```

### Read More
- [makeSubTotal method](../core/make-sub-total) 

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
