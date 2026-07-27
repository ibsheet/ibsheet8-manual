# DefaultValue ***(col)***
> 컬럼에 기본 값을 설정합니다.
>
> 신규행을 추가하거나 조회데이터 안에 해당 열에 대한 데이터가 없는 경우, 지정한 값이 자동으로 표시됩니다.
>
> 특히 `Button` 타입 사용시 버튼에 기본적으로 표시될 내용을 설정하면, 별도로 버튼 컬럼에 대한 조회가 없어도 해당 값이 표시됩니다. 
>
> 값을 읽거나(getValue) 저장하거나 엑셀로 다운로드할 때는 DefaultValue 값으로 처리됩니다. 
>
> 해당 속성에 영향을 받는 데이터는 아래와 같습니다.
```javascript
{Type: "Text", Name: "sText", DefaultValue : "홍길동"}

data: [
    {"e": null},      //null 데이터
    {"e": undefined}, //undefined 데이터
    {}                //데이터 없음 
]
```
`CanEmpty`를 설정하지 않은 컬럼에서 `DefaultValue`와 `EmptyValue`를 동시에 설정한 경우, <br/>
- 데이터가 `null`, `undefined`, `테이터 없음`은 `DefaultValue`가 우선 적용됩니다.<br/>
- 빈문자열("")은 `EmptyValue`가 적용 됩니다.<br/>

`CanEmpty:1` 설정한 컬럼에서는 `DefaultValue` 설정은 무시됩니다.<br/>

### Type
`mixed`

### Options
|Value|Description|
|-----|-----|
|`mixed`|신규 행이나 조회시 값이 없을때 기본값으로 표시할 내용|

### Example
```javascript
//버튼 컬럼에 기본 타이틀 지정
options.Cols = [
    {Header: "상세정보", Type: "Button", Name: "DetailBnt", Button: "Button", DefaultValue: "확인"},
    ...
];
```
![Default](/assets/imgs/button5.png)<br/>
상세보기 컬럼에 조회 데이터가 없어도 "확인"이 표시됩니다.

### Read More
- [EmptyValue col](./empty-value)
- [SpaceForDefaultValue cfg](/docs/props/cfg/space-for-default-value)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
