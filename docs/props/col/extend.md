# Extend ***(col)***

<!-- synonyms: 열 상속, 컬럼 설정 재사용, 공통 열 규격, 열 템플릿, 컬럼 확장, extend column, column inherit, common column config, template column -->

> 시트 생성 시 `Cols`에 들어가는 열 설정([Type (col)](/docs/props/col/type), [Format (col)](/docs/props/col/format) 등)을 다른 변수에서 가져와 적용합니다.  
> 예를 들어 "`$` 표시 + 천 단위 콤마 + 너비 120px 고정" 같은 공통 규격을 변수에 미리 정의해 두면, 그 규격이 필요한 모든 열에서 변수를 `Extend`로 불러와 똑같이 적용할 수 있습니다.  
> 변수의 정의 위치는 자유이며, 배포 파일 `ibsheet-common.js`에는 날짜 형식 등 자주 쓰는 설정이 `IB_Preset`으로 기본 제공됩니다. 프로젝트에 필요한 설정도 여기에 추가해 사용할 수 있습니다.  
> `Extend`는 시트 생성(create) 시에만 적용되며, 이미 생성된 시트에는 반영되지 않습니다.

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

같은 속성을 직접 설정과 `Extend`에 모두 지정하면 `Cols` 항목에서 **뒤에 쓴 값**이 적용됩니다. (헤더 `Header`는 순서와 무관하게 직접 지정한 값이 우선)

```javascript
var defaultWidth = {Width: 100, MinWidth: 70};
var options = {
    Cols:[
        {Width: 300, Extend: defaultWidth},  //너비가 100px로 설정됨
        {Extend: defaultWidth, Width: 300}   //너비가 300px로 설정됨
    ]
}
```

### 기본 제공 프리셋 (IB_Preset)
`ibsheet-common.js`에 정의되어 있어 별도 정의 없이 `Extend`로 바로 사용할 수 있습니다.

**날짜/시간**
|프리셋|표시 형식|
|---|---|
|`YMD`|yyyy/MM/dd|
|`YM`|yyyy/MM|
|`MD`|MM/dd|
|`HMS`|HH:mm:ss|
|`HM`|HH:mm|
|`YMDHMS`|yyyy/MM/dd HH:mm:ss|
|`YMDHM`|yyyy/MM/dd HH:mm|
|`MDY`|MM-dd-yyyy|
|`DMY`|dd-MM-yyyy|

**숫자**
|프리셋|표시 형식|설명|
|---|---|---|
|`Integer`|#,##0|정수 (0을 `0`으로 표시)|
|`NullInteger`|#,###|정수 (값이 0이면 빈칸)|
|`Float`|#,##0.######|실수 (0을 `0`으로 표시)|
|`NullFloat`|#,###.######|실수 (값이 0이면 빈칸)|

**기능**
|프리셋|용도|
|---|---|
|`Popup`|편집 가능한 셀에 팝업 버튼 표시|
|`STATUS`|행의 저장 상태 표시 (입력/수정/삭제)|
|`DelCheck`|체크박스로 행을 삭제 상태로 전환|

`STATUS`, `Popup`은 내부적으로 Formula를 사용하므로 [Def.Row](/docs/start/basic-structure)에 [CanFormula (row)](/docs/props/row/can-formula)와 [CalcOrder (row)](/docs/props/row/calc-order)를 **둘 다 반드시** 설정해야 합니다. `CalcOrder`에는 계산할 대상을 지정하며, 값을 계산하는 `STATUS`는 `열이름`, 셀 속성을 계산하는 [attribute+Formula (col)](/docs/props/col/attribute-formula)(예: `Popup`의 `ButtonFormula`)는 `열이름+속성명` 형식으로 적습니다. (`DelCheck`는 이벤트로 동작해 둘 다 필요 없습니다.)

```javascript
options.Def = { Row: { CanFormula: 1, CalcOrder: "status,deptButton" } };
//CanFormula와 CalcOrder를 함께 설정 (CalcOrder 항목 사이에는 공백을 넣지 않음)
options.Cols = [
    {Header: "상태", Name: "status", Extend: IB_Preset.STATUS},   //값 Formula → 열이름 "status"
    {Header: "부서", Name: "dept",   Extend: IB_Preset.Popup},    //ButtonFormula → 열이름+속성명 "deptButton"
    {Header: "삭제", Name: "del",    Extend: IB_Preset.DelCheck}  //이벤트 → CalcOrder 불필요
];
```

자세한 사용법은 [STATUS](/docs/migration/migration-06-01), [Popup](/docs/migration/migration-06-06), [DelCheck](/docs/migration/migration-06-02) 문서를 참고하세요.

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
