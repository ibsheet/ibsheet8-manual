# NoDataMiddle ***(cfg)***

> 조회된 데이터가 없는 경우 표시되는 NoData행을 화면 가운데에 표시합니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|NoData행을 상단에 표시 (`default`)|
|`1(true)`|NoData행을 화면 가운데에 표시|

NoDataMiddle : 0 (`default`)  
![NoDataMiddle:0](/assets/imgs/NoDataMiddle0.png "NoDataMiddle:0")

NoDataMiddle : 1  
![NoDataMiddle:1](/assets/imgs/NoDataMiddle.png "NoDataMiddle:1")


### Example
```javascript
options.Cfg = {
  NoDataMiddle: 1,  // 조회된 데이터가 없는 경우 화면 가운데에 표시
  ...
};
```

### Read More
- [NoDataMessage cfg](/docs/props/cfg/no-data-message)

### Since

|product|version|desc|
|---|---|---|
|core|8.1.0.36|기능 추가|
