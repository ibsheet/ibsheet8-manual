# EmptyValue ***(col)***

<!-- synonyms: 빈값 표시, placeholder, 값 없을 때 표시, 빈 셀 문구, 힌트 텍스트, empty value, placeholder text, blank display, no value text -->

> 셀에 값이 없을때 보여질 글자를 설정합니다.
>
> `Html` input 객체의 `placeholder`속성과 비슷한 기능으로, 값을 읽거나(getValue) 저장하거나 엑셀로 다운로드할 때는 값이 없는 상태로 처리됩니다. 
>
> 해당 속성에 영향을 받는 데이터는 아래와 같습니다.
```javascript
{Type: "Text", Name: "sText", EmptyValue : "값이 없습니다."}

data: [
    {"e": null},      //null 데이터
    {"e": undefined}, //undefined 데이터
    {"e": ""},        //빈문자 데이터
    {}                //데이터 없음 
]
```
`CanEmpty`를 설정하지 않은 컬럼에서 `DefaultValue`와 `EmptyValue`를 동시에 설정한 경우, <br/>
- 데이터가 `null`, `undefined`, `테이터 없음`은 `DefaultValue`가 우선 적용됩니다.<br/>
- 빈문자열("")은 `EmptyValue`가 적용 됩니다.<br/>

`CanEmpty:1` 설정한 컬럼에서는 `DefaultValue` 설정은 무시됩니다.<br/>

### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`string`|신규 행이나 조회시 값이 없을때 보여질 내용|


### Example
```javascript
//필수 입력에 대한 안내를 설정
options.Cols = [
    ...
    {Type: "Text", Name: "sa_point", EmptyValue: "필수 입력항목 입니다.", ...},
    ...
];

```

### Read More
- [CanEmpty col](./can-empty)
- [DefaultValue col](./default-value)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
