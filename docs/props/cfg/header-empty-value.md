# HeaderEmptyValue ***(cfg)***

<!-- synonyms: 빈 헤더, 공백 헤더, 헤더 Name 노출, 헤더 이름 표시, empty header, header blank -->

> 헤더행의 셀 값이 없거나 공백 문자열일 때, 컬럼 `Name` 값으로 대체하지 않고 그대로 공백으로 표시할지 설정합니다.

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

### Read More
- [Header col](/docs/props/col/header)
- [Name col](/docs/props/col/name)

### Since

|product|version|desc|
|---|---|---|
|core|8.3.0.62|기능 추가|
