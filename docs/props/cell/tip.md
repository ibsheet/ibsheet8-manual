# Tip ***(cell)***
> 셀 위에 마우스 커서 오버 시 풍선도움말을 표시할지 여부와,
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
|`0(false)`|풍선도움말 사용 안함(`Default`)|
|`1(true)`|풍선도움말 사용|
|`string`|풍선도움말에서 표시 될 내용 설정|

### Example
```javascript

//1. 메소드를 통해 특정 셀에 속성 적용 (열이름: CLS)
sheet.setAttribute(sheet.getRowById("AR1"), "CLS", "Tip", 1);


//2. 객체에 직접 접근해서 속성 적용 (열이름: CLS)
var ROW = sheet.getRowById("AR10");
ROW["CLSTip"] = 1;

//3.HTML 태그를 사용하여 풍선도움말 내용을 구성
var row = sheet.getRowById("AR2");
row["CLSTip"] = "<b>결제 완료</b><br/>" +
           "<span style='color:red;'>취소가 불가능한 건입니다.</span>";


//4. 조회 데이터 내에서 속성 적용 (열이름: CLS)
{
    data:[
        {... , "CLSTip":"작업 시작일과 종료일을 입력해 주세요." , ...}
    ]
}
```

### Read More
- [Tip+Value cell](./tip-value)
- [TipClass cell](./tip-class)
- [StandardTip cfg](/docs/props/cfg/standard-tip)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
