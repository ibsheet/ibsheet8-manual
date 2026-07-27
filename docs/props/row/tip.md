# Tip ***(row)***

> 행 위에 마우스 커서 오버 시 풍선도움말을 표시할지 여부와,
> 풍선도움말에 표시될 내용을 설정합니다.
> 
> Tip 값을 `1(true)`로 설정하면, 해당 셀의 데이터 값이 풍선도움말 내용으로 자동 표시됩니다.
> 
> - Tip 값이 문자열인 경우, 기본적으로 HTML 태그를 사용하여 풍선도움말 내용을 구성할 수 있습니다.
> - 단, [StandardTip](/docs/props/cfg/standard-tip)의 값이 `1(true)`인 경우에는
> 브라우저의 내장 툴팁을 사용하게 되어 HTML 태그는 표현되지 않습니다.

###
![Tip](/assets/imgs/tip.png "Tip 사용")

### Type
`mixed`( `boolean` \| `string`)

### Options
|Value|Description|
|-----|-----|
|`0(false)`|풍선도움말 사용 안함(`Default`)|
|`1(true)`|풍선도움말 사용|
|`string`|풍선도움말에서 표시 될 내용 설정|

### Example
```javascript
//1. 55번 행에 마우스 오버시 풍선 도움말에 표시될 내용을 변경.
var row = sheet.getRowById("AR55");
row["Tip"] = "해당 건은 결제가 완료되었습니다.";

//2.HTML 태그를 사용하여 풍선도움말 내용을 구성
var row = sheet.getRowById("AR2");
row["Tip"] = "<b>결제 완료</b><br/>" +
           "<span style='color:red;'>취소가 불가능한 건입니다.</span>";

//3. 2번 행에 마우스 오버시 셀 데이터 내용으로 풍선 도움말 표시
var row = sheet.getRowById("AR2");
row["Tip"] = 1;

//4. 함수를 이용하여 풍선 도움말 표시
var row = sheet.getRowById("AR2");
sheet.setAttribute(row, null, "Tip", 1);

//5. 조회 데이터에서 일부 행에 대해 풍선도움말 기능을 제거.
{"data":[
    {"Tip": 0, "ColName1": "Value1", "ColName2": "Value2", ...},
    ...
]}
```

### Read More
- [TipClass row](./tip-class)
- [TipPosition row](./tip-position)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
