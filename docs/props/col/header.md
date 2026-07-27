# Header ***(col)***
> 열의 헤더 셀을 정의합니다.
>
> 헤더 셀에는 단순 문자열을 넣거나, 배경색과 정렬(alignment) 등 속성을 함께 설정할 수 있습니다.
>
> 여러 개의 헤더 행을 만들려면 배열로 설정하며, **컬럼별 배열 길이는 동일**해야 합니다. 
>
> **<mark>주의</mark>** : Header를 string로 설정시 빈 헤더를 설정하려면 공백 문자열을 사용해야 합니다.
>
> Header:"<mark> </mark>"


### Type
`mixed`( `string` \| `object` \| `array`\[`string`\|`object`\] )


### Options
|Value|Description|
|-----|-----|
|`string`|헤더셀에 들어갈 타이틀<br/>`\n`으로 줄바꿈 가능|
|`object`|타이틀과 정렬, 배경색, 글자색 등을 함께 설정|
|`array`\[`string`\|`object`\]|다중 헤더 행을 구성할 경우 배열로 설정|

### Example
한줄 헤더행 예)
```javascript
options.Cols = [
    {   
        // string 형태로 단순 타이틀
        Header: "사원명", // "사원\n명" → 줄바꿈 표시
        Type: "Text", MinWidth: 120, Name: "sa_name"
    },
    {  
        // object 형태로 배경색, 글자색, 정렬 지정
        Header: {Value: "부서", Color: "#EDEDED", TextColor: "#FF0000", Align: "Left"},
        Type: "Text", MinWidth: 120, Name: "deptCd"
    }
];
```
!["한줄헤더"](/assets/imgs/headerSingleRow.png)<br/>



다중 해더행 예)
```javascript
options.Cfg = {HeaderMerge: 3}; //헤더 영역 머지모드
options.Cols = [
    {
        Header: ["사원정보", "이름"], // String 형태
        Type: "Text", MinWidth: 120, Name: "sa_name"
     },
    {
        Header: ["사원정보","사번"],
        Type: "Text", MinWidth: 80, Name: "sa_no"
    }
]

// 또는 object 형태로 스타일 포함

options.Cfg = {HeaderMerge: 3}; //헤더 영역 머지모드
options.Cols = [
    {
        Header:[
            {Value: "사원정보", Align: "Center"},
            // Object 형태로 배경이나 글자색,정렬등을 같이 설정하는 방법
            {Value: "이름", Color: "#315C81", TextColor: "#FFEEFF", Align: "Left"}
        ],
        Type: "Text", MinWidth: 120, Name: "sa_name"
     },
    {
        Header:[
            {Value: "사원정보"},
            {Value: "사번", Color: "#315C81", TextColor: "#ED6655", Align: "Left"}
        ],
        Type: "Text", MinWidth: 80, Name: "sa_no"
    },
];
```
!["두줄헤더"](/assets/imgs/headerDoubleRow.png)<br/>

### Read More
- [HeaderMerge cfg](/docs/props/cfg/header-merge)
- [Span cell](/docs/props/cell/span)
- [RowSpan cell](/docs/props/cell/row-span)
### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
