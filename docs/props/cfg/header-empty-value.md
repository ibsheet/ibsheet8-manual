# HeaderEmptyValue ***(cfg)***

> 헤더행의 셀 값이 없거나 공백 문자열인 경우 그대로 공백 설정 되도록 설정하는 기능입니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0`|헤더행의 셀 값이 없거나 공백 문자열인 경우 `Name` 속성의 값이 채워짐 (`default`)|
|`1`|헤더행의 셀 값이 그대로 공백으로 설정|

### Example
```javascript
options.Cfg = {
    HeaderEmptyValue: 1
};

options.Cols = [
    {
        Type: "Text",
        Name: "TextData",
        Header: "", // 헤더행 셀 값을 공백으로 설정
    }
]
```


### Since

|product|version|desc|
|---|---|---|
|core|8.3.0.62|기능 추가|
