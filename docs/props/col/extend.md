# Extend ***(col)***

<!-- synonyms: 열 상속, 컬럼 설정 재사용, 공통 열 규격, 열 템플릿, 컬럼 확장, extend column, column inherit, common column config, template column -->

> 시트 생성시 Cols에 들어가는 열 설정([Type (col)](/docs/props/col/type), [Format (col)](/docs/props/col/format) 등)을 다른 변수로부터 가져와 적용합니다.
>
> 가령 프로젝트에서 달러를 표시하는 열에 대한 공통 규격을 아래와 같이 정했다고 가정합니다.
>
> 1. 숫자 앞에 "$"기호를 표시.
> 2. 3자리 숫자 마다 ","가 보여지고, 소숫점 이하 1번째 자리까지만 표현.
> 3. 열의 너비는 120px 이고 열의 너비는 사용자가 조절하지 못하게 끔 할 것.
> 4. 배경색을 "#FFFF88"으로 표현.
>
> 이 경우 모든 프로젝트의 개발자가 위 내용을 숙지하여 달러가 표현되야 하는 모든 열에 대해서 [Type (col)](/docs/props/col/type), [Format (col)](/docs/props/col/format), [Width (col)](/docs/props/col/width) 등을 설정하는 것보다, 이러한 설정 정보를 미리 변수에 담아두고 해당 열을 만들때 변수의 내용을 적용하게 끔 한다면 훨신 쉽게 동일한 형태의 열을 만들 수 있습니다.
>
> 이렇게 `Extend` 속성은 공통 변수에 담긴 열 설정 정보를, 해당열에 적용시키는 기능을 합니다.
> 이런 공통 열 설정은 화면에서 접근할 수 있는 변수에 미리 정의해 두기만 하면 되고, `Extend`는 그 값을 읽어와 적용할 뿐입니다. 정의 위치는 자유입니다.  
> 배포 파일에 함께 들어 있는 `ibsheet-common.js`에는 `IB_Preset`으로 날짜 형식 프리셋(`YMD`, `YMDHMS` 등)이 예시로 정의돼 있으며, `USD`처럼 프로젝트에서 필요한 설정은 여기에 직접 추가해 함께 사용합니다.
> `Extend` 속성은 시트 생성시(create)에만 설정 가능하며, 이미 생성된 시트에는 적용되지 않습니다.
>
> **주의 : 같은 속성을 직접설정과 `Extend`에 모두 주면 `Cols` 항목에서 뒤에 쓴 값이 이깁니다. 단, 헤더(`Header`)는 순서와 무관하게 직접 지정한 값이 우선합니다.**

```javascript
var defaultWidth = {Width: 100, MinWidth: 70};
var options = {
    Cols:[
        {Width: 300, Extend: defaultWidth},  //너비가 100px로 설정됨
        {Extend: defaultWidth, Width: 300}   //너비가 300px로 설정됨
    ]
}
```


### Type
`object`

### Options
|Value|Description|
|-----|-----|
|`object`|[LeftCols, Cols, RightCols](/docs/start/basic-structure)에 들어가는 설정값 들|


### Example
```javascript
//프로젝트 공통으로 사용할 열 설정 정보를 변수에 정의해 둡니다.(ibsheet-common.js파일 참고)
var IB_Preset = {
    USD:{Type: "Float", Format: "$ #,##0.#", Width: 120, CanResize: 0,Color: "#FFFF88"},  //미화 표시
    YMD:{Type: "Date", Format: "yyyy-MM-dd", EditFormat: "yyyyMMdd", Width: 110}, //년월일 기본 표시
    REGD:{Type: "Date", Format: "yyyy-MM-dd HH:mm", DataFormat: "yyyyMMddHHmm",CanEdit: 0, Width: 150}, //작성일시
    ... 여러가지 열 형식을 미리 정의해 둔다 ...
};

//시트 생성시 Extend를 이용하여 열 생성
//(Name속성만 설정하고 나머지 설정은 Extend로 반영받는다.)
options.Cols = [
    //Type,Format 등이 모두 한꺼번에 적용된다.
    {Name: "exportIncom", Extend: IB_Preset.USD},
    {Name: "birthDate", Extend: IB_Preset.YMD, CanEdit: 1},
    {Name: "ModiDate", Extend: IB_Preset.REGD},
    ...
];
```

### Try it
- [Demo of Extend](https://jsfiddle.net/gh/get/library/pure/ibsheet/ibsheet8-manual-sample/tree/master/samples/properties/Col/Extend/)

### Read More
- [Type col](/docs/props/col/type)
- [Format col](/docs/props/col/format)
- [DataFormat col](/docs/props/col/data-format)
- [EditFormat col](/docs/props/col/edit-format)
- [Width col](/docs/props/col/width)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
