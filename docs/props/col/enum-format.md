# EnumFormat ***(col)***

<!-- synonyms: Enum 마스킹, 콤보 포맷, Enum 표시 형식, 드롭다운 포맷, enum format, dropdown format, combo mask, enum display format -->

> Enum 컬럼 데이터에 대한 마스킹을 정의합니다.


### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`function`|return 값을 기준으로 Enum 컬럼 데이터에 관한 마스킹 표시|


### Example
```javascript

options.Cols = [
    ...
    //임의의 함수로 처리
    {Type: "Enum", Name: "EnumData", Enum: "|토마토|감자|옥수수", Range: 1, EnumFormat: function (param, sheet, col) {
        if (param.indexOf(";") == -1 || param == "&#160;") return param;
        var valArr = param.split(";");
        var length = valArr.length - 1 + "";
        // '토마토;감자'로 val 값이 들어올 경우, '토마토 외 1건'과 같은 형식으로 표시한다.
        return valArr[0] + " 외 " + length + "건";
    }},
    ...
];
```

### Read More
- [Enum](./enum)
- [Format appendix](/docs/appx/format)
- [Format col](./format)

### Since

|product|version|desc|
|---|---|---|
|core|8.2.0.9|기능 추가|