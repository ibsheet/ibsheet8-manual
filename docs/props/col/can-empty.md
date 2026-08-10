# CanEmpty ***(col)***

<!-- synonyms: 빈 값 허용, null 허용, 공백 허용, 빈값 표시, undefined 허용, 빈 셀 허용, empty value, allow null, allow empty, nullable, blank allowed -->

> `Int`, `Float`, `Bool`, `Date` 타입에서 데이터의 값이 없을 경우, 빈값으로 표시될 수 있도록 하는 설정입니다.<br/> `CanEmpty: 0`으로 설정된 열에 대해서는 값을 지우거나 빈 값으로 설정할 수 없습니다.
>
> 해당 속성에 영향을 받는 데이터는 아래와 같습니다.
```javascript
{Type: "Int", Name: "sInt", CanEmpty: 1}

data: [
    {"sInt": null},      //null 데이터
    {"sInt": undefined}, //undefined 데이터
    {}                   //데이터 없음
]
```
<!-- `Bool` 타입의 경우 1번부터 4번까지 값 사이클은 다음과 같습니다.<br/>
 1 인 경우 `["" => 1 => 0 ...]` , 2 인 경우 `["" => 0 => 1 ...]`,<br/>
3 인 경우 `"" => [1 => 0 => 1 => 0 ...]`, 4 인 경우 `"" => [0 => 1 => 0 => 1 ...]` 형태로 `Bool` 타입의 값이 싸이클을 돕니다. <br/>-->

### 빈데이터 기본값 표시
| | Bool| Int| Float| Date|
|-- | -- | -- |-- |-- |
|CanEmpty : 0|   0(unCheck)  |   0 |0 |19700101|
|CanEmpty : 1|   ""  |   "" |"" |""|


**CanEmpty : 0** <br/>
![CanEmpty0](/assets/imgs/CanEmpty0.gif "CanEmpty0")<br/>
**CanEmpty : 1** <br/>
![CanEmpty1](/assets/imgs/CanEmpty1.gif "CanEmpty1")<br/>
<!-- **CanEmpty : 2** <br/>
![CanEmpty2](/assets/imgs/CanEmpty2.gif "CanEmpty2")<br/>
**CanEmpty : 3** <br/>
![CanEmpty3](/assets/imgs/CanEmpty3.gif "CanEmpty3")<br/>
**CanEmpty : 4** <br/>
![CanEmpty4](/assets/imgs/CanEmpty4.gif "CanEmpty4")<br/>
-->
### 
### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`0`|빈 값 설정 불가 (default: `Int`, `Float`, `Bool`)|
|`1`|빈 값 설정 가능 (default: `Date`)|

<!--! 
|`2`|빈 값 설정 가능 (사용: `Bool`)|
|`3`|빈 값 설정 가능 (사용: `Bool`)|
|`4`|빈 값 설정 가능 (사용: `Bool`)|
!-->


### Example
```javascript
// 특정 열에 대해 빈 값이 설정되도록 수정
options.Cols = [
    {Type: "Int", Name: "sPoint", CanEmpty: 1 ...},
    {Type: "Bool", Name: "sBool1", CanEmpty: 1 ...},
    ...
];
```

### Read More
- [CanEdit col](./can-edit)
- [CanMove col](./can-move)
- [CanResize col](./can-resize)
- [CanSort col](./can-sort)
- [EmptyValue col](./empty-value)
- [Type col](/docs/props/col/type)
- [Type appendix](/docs/appx/type)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
