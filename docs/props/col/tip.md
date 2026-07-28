# Tip ***(col)***
> 열 위에 마우스 커서 오버 시 풍선도움말을 표시할지 여부와,
> 풍선도움말에 표시될 내용을 설정합니다.
> 
> Tip 값을 `1(true)`로 설정하면, 해당 셀의 데이터 값이 풍선도움말 내용으로 자동 표시됩니다.
> 
> - Tip 값이 문자열인 경우, 기본적으로 HTML 태그를 사용하여 풍선도움말 내용을 구성할 수 있습니다.
> - 단, [StandardTip](/docs/props/cfg/standard-tip)의 값이 `1(true)`인 경우에는
> 브라우저의 내장 툴팁을 사용하게 되어 HTML 태그는 표현되지 않습니다.

### Type
`mixed`( `boolean` \| `string` )

### Options
|Value|Description|
|-----|-----|
|`0(false)`|풍선도움말 사용 안함 (`default`)|
|`1(true)`|풍선도움말 사용|
|`string`|풍선도움말에서 표시 될 내용 설정|

### Example
```javascript

//1. 특정 열에 풍선도움말 기능 활성화 (열의 셀 데이터 값이 풍선도움말로 표시됨)
options.Cols = [
    ...
    {Type: "Text", Tip: 1, Name: "DESC", Width: 120 ...},
    ...
];

//2. 함수를 이용하여 특정 열에 사용자 정의 풍선도움말 설정
var tipString = "<b>결제 완료</b><br/>" +
           "<span style='color:red;'>취소가 불가능한 건입니다.</span>";

sheet.setAttribute(null, "DESC", "Tip",tipString);

```

### Read More
- [Tip+Value col](./tip-value)
- [TipClass col](./tip-class)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
