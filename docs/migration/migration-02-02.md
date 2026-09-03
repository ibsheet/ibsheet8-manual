# 초기화 구문 변경

<!-- synonyms: IBSheet7, 마이그레이션, sheet7, migration, v7, v8, ibsheet7에서 ibsheet8로, 초기화 구문, SetConfig, InitHeaders, InitColumns, options, Cfg 설정, 시트 옵션, initialization -->

기존 IBSheet7의 각 열 별 타입, 포맷, 기능에 대해서 IBSheet8에서 변경된 내용을 아래에서 확인해 보세요.

**주요 초기화 기능 변경**

**전역 공통 설정 파일 (`ibsheet.cfg`)**

IBSheet7은 `ibsheet.cfg` 파일에서 모든 시트에 공통으로 적용되는 전역 설정을 관리했습니다.  
IBSheet8에는 `ibsheet.cfg` 파일이 없습니다.  
모든 시트에 공통으로 적용할 설정은 `ibsheet-common.js`에서 [IBSheet.CommonOptions (static)](/docs/static/common-options)에 지정합니다.  
`CommonOptions`에 둔 `Cfg`, `Def`, `Events` 값은 각 화면에서 생성하는 시트 초기값과 머지되어 적용되며, 값이 다르면 화면별 설정이 우선합니다.

```javascript
// ibsheet-common.js 등에서 (ibsheet.js 로드 이후에 설정)
IBSheet.CommonOptions = {
    Cfg: {
        // 모든 시트에 공통 적용할 Cfg (IBSheet7 ibsheet.cfg 전역 설정 대체)
        Alternate: 2,
        InfoRowConfig: { Visible: 1 }
    }
};
```

***Cfg(SetConfig)***

|IBSheet7 속성|기능 설명|IBSheet8 대응|
|---|---|---|
|AutoFitColWidth|지정한 시점마다 각 열의 너비를 가로 스크롤바가 생기지 않는 범위 내로 조정해 주는 기능|[AutoFitColWidth (cfg)](/docs/props/cfg/auto-fit-col-width) 속성으로 동일하게 사용|
|CountFormat,CountPosition,PagingPosition|조회된 데이터 건수 표시 기능|[InfoRowConfig (cfg)](/docs/props/cfg/info-row-config) 속성을 통해 설정|
|DragMode|드래그 방식,가능 여부 설정| [CanDrag (cfg)](/docs/props/cfg/can-drag) 속성을 통해 설정 가능|
|HeaderRowHeight,DataRowHeight|헤더,데이터 행의 높이를 설정|css 를 통해 설정하는 형태로 변경<br/>[Size (cfg)](/docs/props/cfg/size)를 통해 시트의 행 높이, 아이콘 크기, 버튼 크기 등 전체적인 크기 조절이 가능|
|FrozenCol,FrozenColRight|좌우측 열고정 기능|[LeftCols, RightCols](/docs/start/basic-structure) 속성을 통해 시트 생성시 설정. 이후로는 [setFixedCols (method)](/docs/funcs/core/set-fixed-cols) 함수로 변경가능|
|MergeSheet|헤더, 데이터행의 머지종류 설정|[HeaderMerge (cfg)](/docs/props/cfg/header-merge),[DataMerge (cfg)](/docs/props/cfg/data-merge), [PrevColumnMerge (cfg)](/docs/props/cfg/prev-column-merge) 속성으로 변경|
|Page|한번에 렌더링할 행의 개수|[PageLength (cfg)](/docs/props/cfg/page-length)로 명칭 변경|
|ReverseSortOrder|헤더 클릭 시 다중 정렬 처리 방법(정렬 우선순위) 설정|[HeaderSortMode (cfg)](/docs/props/cfg/header-sort-mode)로 대체 (클릭 순서대로 정렬은 `HeaderSortMode:4`)|
|SearchMode|조회 렌더링 방식 설정|[SearchMode (cfg)](/docs/props/cfg/search-mode) 속성으로 동일하지만 Mode는 조금씩 다르며 일부 모드는 추가됨|
|SumPosition|합계 행에 대한 위치|[setFormulaRowPosition (method)](/docs/funcs/core/set-formula-row-position) 함수를 통해 설정|
|ToolTip|풍선도움말 사용여부|row,col 속성 설정에서 `Tip` [(row)](/docs/props/row/tip) [(col)](/docs/props/col/tip) [(cell)](/docs/props/cell/tip)으로 변경|
|UseHeaderActionMenu|헤더행 컨텍스트 메뉴 기능|IBSheet8은 헤더 컨텍스트 메뉴를 기본 제공하며, [UseHeaderContextMenu (cfg)](/docs/props/cfg/use-header-context-menu)로 표시 여부를 제어. 메뉴 항목을 직접 구성하려면 [Def/Header](/docs/start/basic-structure)에 [Menu](/docs/appx/menu) 속성으로 설정|

***Cols(InitColumns)***

### [Type](/docs/appx/type) 속성
|IBSheet7 Type|IBSheet8 대응|
|---|---|
|Text|일반 문자형 타입으로 동일합니다.|
|Status|지원안함<br/>`Status`타입 열의 유무와 상관없이 시트 내에 변경사항에 대한 관리가 자동으로 이루집니다.<br/> 일반적으로 수정된 행은 노란색(`.IBColorChanged`),입력은 파란색(`.IBColorAdded`),삭제는 붉은색(`.IBColorDeleted`) 배경색으로 변경되어 표시 됩니다.<br/>서버로 전송되는 행 상태에 대한 값은 기본적으로 'STATUS' 로 전송되며 이름을 변경하고 싶은 경우에는 Cfg에서 `ReqStatusName` 속성으로 변경할수 있습니다.<br/>기존에 `I`, `U`, `D`로 서버로 전송되던 값은 `Added`, `Changed`, `Deleted` 로 전송됩니다.<br/> 이를 기존과 동일한 `I`, `U`, `D`로 변경하시려면 ko.js(메세지파일)에서 `ReqStatusAdded`, `ReqStatusChanged`, `ReqStatusDeleted`를 `I`, `U`, `D`로 수정해 주세요.<br/>기존 IBSheet7과 마찬가지로 사용자에게 행의 입력/수정/삭제 여부를 별도 열을 통해 표시하고자 하는 경우에는 아래 [Status 타입 마이그레이션](/docs/migration/migration-06-01) 부분을 참고해 주세요.|
|DelCheck|지원안함<br/> `deleteRow()`함수를 통해서 행의 상태를 삭제로 변경할 수 있습니다.<br/>IBSheet7처럼 체크박스를 두고 상태를 삭제로 변경하고자 하신다면 열의 Type을 `Bool`로 설정하시고 [OnChange (json event)](/docs/props/event/on-change)를 통해 행의 상태를 바꾸게끔 설정하시면 됩니다.<br/>자세한 코드는 아래 [DelCheck 타입 마이그레이션](/docs/migration/migration-06-02) 부분 참고해주세요.|
|CheckBox|`Bool`타입으로 변경되었습니다.|
|DummyCheck|지원안함<br/>`Bool` 타입으로 설정하고 [NoChanged (col)](/docs/props/col/no-changed) 속성을 1로 설정하시면 됩니다.|
|Radio| `Radio`로 동일합니다.|
|Combo| `Enum` 타입으로 변경되었습니다. <br/>콤보의 item을 설정하던 `ComboText`, `ComboCode`는 각각 [Enum (col)](/docs/props/col/enum), [EnumKeys (col)](/docs/props/col/enum-keys)로 변경되었습니다.<br/>특히 `Enum`, `EnumKeys`의 첫번째 글자를 구분자로 사용하는 것을 주의해 주세요.<br/>보다 자세한 내용은 아래 [Combo,ComboEdit 타입 마이그레이션](/docs/migration/migration-06-03)을 참고해 주세요.|
|ComboEdit|지원안함.<br/>[Combo,ComboEdit 타입 마이그레이션](/docs/migration/migration-06-03)을 참고해 주세요.|
|AutoSum|타입은 Int나 Float으로 설정하시고, [FormulaRow (col)](/docs/props/col/formula-row) 속성을 사용하시면 합계나 평균을 표시할 수 있습니다.|
|Image|`Img`타입으로 변경되었습니다.<br/>특히 데이터 구조가 크게 변경되었으므로 [Type](/docs/appx/type)부분의 내용을 참고해 주세요.|
|Int|`Int`로 동일합니다.|
|Float|`Float`로 동일합니다.|
|Date|`Date`로 동일합니다. 단 `Type:"Date"`만 지정하면 날짜가 원하는 형식으로 표시되지 않으므로 [Format (col)](/docs/props/col/format), [DataFormat (col)](/docs/props/col/data-format), [EditFormat (col)](/docs/props/col/edit-format) 세 속성을 반드시 함께 지정해야 합니다.<br/>날짜 구분자(예: `yyyy.MM.dd` → `yyyy-MM-dd`)를 변경하려는 경우에도 위 세 속성을 함께 설정합니다.<br/>예: `Format:"yyyy.MM.dd"`, `DataFormat:"yyyyMMdd"`, `EditFormat:"yyyyMMdd"`<br/>자세한 사항은 아래 Format 속성을 참고하세요.|
|Popup|지원안함.<br/>열 우측에 버튼을 두고자 하시는 경우에는 `Button`속성을 통해 설정하실 수 있습니다.<br/>ex) {Type:"Text",Name:"DEPTPOP",`Button:"../assets/imgs/popup.png"`}<br/>버튼 클릭시 발생하는 이벤트는 [onButtonClick (event)](/docs/events/on-button-click)을 참고하세요.<br/>또는 `IB_Preset.Popup`을 [Extend](/docs/props/col/extend)하시면 ibsheet7 Popup 모양을 그대로 재현할 수 있습니다. 자세한 코드는 아래 [Popup 타입 마이그레이션](/docs/migration/migration-06-06) 부분 참고해주세요.|
|Pass|`Pass`로 동일합니다.|
|Seq|지원안함<br/> 열의 타입을 Int로 설정하시고, `Name`을 `"SEQ"`로 지정하시면 자동 순번열 형태로 동작합니다.|
|Html|`Html`로 동일합니다.|
|Button|`Button`으로 동일합니다.<br/>단 [onButtonClick (event)](/docs/events/on-button-click)이벤트 대신 [onClick (event)](/docs/events/on-click)이벤트를 통해 클릭에 대한 로직을 구성하셔야 합니다.|
|Result|지원안함|
|Sparkline|D3 라이브러리를 이용하여 구현 가능 ([스파크차트 예제 참고](https://www.ibsheet.com/v8/ibsheet/html/examples.html))|


### [Format](/docs/appx/format) 속성
IBSheet7은 `Ymd`, `Integer`, `IdNo`처럼 **이름 하나로 형식을 지정**했으나,  
IBSheet8은 **열의 `Type`(`Date`/`Int`/`Text` 등)을 먼저 정하고 거기에 `Format` 같은 형식 속성을 함께 설정**합니다.  
(형식 패턴, 예약어 등 자세한 내용은 [Format (appendix)](/docs/appx/format) 참고)

|IBSheet7 Format|IBSheet8 대응|
|---|---|
|Ymd, Ym, Md, Hms, Hm, YmdHms, YmdHm|`Type:"Date"` + [Format](/docs/props/col/format)/[DataFormat](/docs/props/col/data-format)/[EditFormat](/docs/props/col/edit-format)<br/>(IBSheet7은 `Text` 타입에도 적용 가능했으나, IBSheet8 날짜 포맷은 `Date` 타입만 지원)|
|Integer, NullInteger, Float, NullFloat|`Type:"Int"`/`"Float"` + [Format (col)](/docs/props/col/format) (`#,##0` 등)|
|IdNo(주민), SaupNo(사업자), PostNo(우편), CardNo(카드), PhoneNo(전화)|`Type:"Text"` + [CustomFormat (col)](/docs/props/col/custom-format) (숫자+구분자 마스크)|
|Number|`Type:"Text"` + [EditMask (col)](/docs/props/col/edit-mask)로 숫자만 입력|

날짜의 경우, 자주 쓰는 포맷 묶음(`Format`/`DataFormat`/`EditFormat`)이 `IB_Preset`에 이미 정의되어 제공되므로  
[Extend (col)](/docs/props/col/extend)로 한 번에 설정할 수 있습니다.
```javascript
//AS-IS
var Cols = [
    {Type:"Date",SaveName:"eDate",Width:100,Format:"Ymd"},
];
```

```javascript
//TO-BE
opt.Cols = [
    //YMD 안에 Type,Width,Format 등이 모두 설정되어 있음.
    {Name:"eDate",Extend:IB_Preset.YMD},
];
```
IB_Preset 변수는 `ibsheet-common.js` 파일 내에 있습니다.  
IBSheet8은 아래 날짜 프리셋을 `ibsheet-common.js`의 `window.IB_Preset`에 **기본 제공**합니다.  
직접 정의하지 않아도 `Extend`로 바로 사용할 수 있으며, IBSheet7에서 쓰던 이름 형식과 아래처럼 대응됩니다.

|IBSheet7 Format|IBSheet8 프리셋|Format(표시)|EditFormat|DataFormat|
|---|---|---|---|---|
|`Ymd`|`IB_Preset.YMD`|`yyyy/MM/dd`|`yyyyMMdd`|`yyyyMMdd`|
|`Ym`|`IB_Preset.YM`|`yyyy/MM`|`yyyyMM`|`yyyyMM`|
|`Md`|`IB_Preset.MD`|`MM/dd`|`MMdd`|`MMdd`|
|`Hms`|`IB_Preset.HMS`|`HH:mm:ss`|`HHmmss`|`HHmmss`|
|`Hm`|`IB_Preset.HM`|`HH:mm`|`HHmm`|`HHmm`|
|`YmdHms`|`IB_Preset.YMDHMS`|`yyyy/MM/dd HH:mm:ss`|`yyyyMMddHHmmss`|`yyyyMMddHHmmss`|
|`YmdHm`|`IB_Preset.YMDHM`|`yyyy/MM/dd HH:mm`|`yyyyMMddHHmm`|`yyyyMMddHHmm`|

이 외에 `IB_Preset.MDY`(`MM-dd-yyyy`), `IB_Preset.DMY`(`dd-MM-yyyy`)도 제공합니다.

숫자 형식도 프리셋으로 제공되며, IBSheet7의 `Integer` 등과 아래처럼 대응됩니다.

|IBSheet7 Format|IBSheet8 프리셋|Format(표시)|설명|
|---|---|---|---|
|`Integer`|`IB_Preset.Integer`|`#,##0`|정수 (0을 `0`으로 표시)|
|`NullInteger`|`IB_Preset.NullInteger`|`#,###`|정수 (값이 0이면 빈칸)|
|`Float`|`IB_Preset.Float`|`#,##0.######`|실수 (0을 `0`으로 표시)|
|`NullFloat`|`IB_Preset.NullFloat`|`#,###.######`|실수 (값이 0이면 빈칸)|

> **프리셋 키는 대소문자를 구분합니다.** IBSheet7의 `Ym`을 `IB_Preset.Ym`으로 쓰면 동작하지 않으며, 반드시 `IB_Preset.YM`(대문자)로 참조해야 합니다.


### 그외에 속성
|IBSheet7 속성|IBSheet8 대응|
|---|---|
|AcceptKeys,ExceptKeys|지원안함<br/>[ResultMask (col)](/docs/props/col/result-mask) 속성을 통해 정규식으로 로직을 구성하셔야 합니다.<br/>기존 코드에 대해 IBSheet8에서 [EditMask (col)](/docs/props/col/edit-mask) 변환하는 코드는 아래 [AcceptKeys,ExceptKeys 마이그레이션](/docs/migration/migration-06-04)을 참고해 주세요.|
|Align|이전과 동일 (center,left,right)|
|AllowNull|[CanEmpty (col)](/docs/props/col/can-empty)로 변경 (`1`이면 숫자 컬럼 빈값 허용)<br/>ex) `{Type:"Int", Name:"amt", CanEmpty:1}`|
|ApproximateType|[DecimalAdjust (col)](/docs/props/col/decimal-adjust)로 변경 (Int/Float 근사값 처리, `round`(기본)/`floor`/`ceil`, 컬럼별 지정 가능. 전역은 [DecimalAdjust (cfg)](/docs/props/cfg/decimal-adjust))<br/>ex) `{Type:"Float", Name:"amt", Format:"#,##0.###", DecimalAdjust:"floor"}`|
|AutoSum|[FormulaRow (col)](/docs/props/col/formula-row) 속성으로 변경. 사용법은 유사하나 함수 연결도 가능해졌습니다.|
|BackColor|[Color (col)](/docs/props/col/color)로 속성명 변경. 사용법은 동일합니다.|
|CalcLogic|[Formula (col)](/docs/props/col/formula) 속성으로 변경. 셀 값 외에 셀/행 속성(색상·편집 가능 여부 등)도 [attribute+Formula (col)](/docs/props/col/attribute-formula)과 [attribute+Formula (row)](/docs/props/row/attribute-formula)로 동적 계산할 수 있게 확장되었습니다.|
|CaseSensitive|[CaseSensitive (col)](/docs/props/col/case-sensitive)로 동일 (필터/정렬 시 대소문자 구분, `0`:구분 안 함 / 기본 `1`)<br/>ex) `{Type:"Text", Name:"sName", CaseSensitive:0}`|
|ClearHeaderCheck|헤더 전체 체크박스만 언체크로 초기화하던 메소드. IB8은 [setAttribute (method)](/docs/funcs/core/set-attribute)로 헤더 셀의 `Checked` 속성을 `0`으로 설정합니다(헤더만 바뀌고 데이터 행은 영향 없음).<br/>ex) `sheet.setAttribute(sheet.Header, "chk", "Checked", 0)`|
|ColMerge|[ColMerge (col)](/docs/props/col/col-merge)속성으로 동일합니다.|
|ComboCode,ComboText|위에 `Combo`, `ComboEdit` 타입에 대한 마이그레이션에서 언급한 것과 같이 [Enum (col)](/docs/props/col/enum), [EnumKeys (col)](/docs/props/col/enum-keys)로 변경되었습니다.<br/>마이그레이션시 IBSheet8에서는 첫번째 글자를 구분자로 사용하는 것을 주의해 주세요.|
|ComboDisabled|[EnumDisabled (col)](/docs/props/col/enum-disabled)로 변경 (Enum 아이템별 선택 불가 설정, 첫 글자 구분자)<br/>ex) `{Type:"Enum", Name:"rel", Enum:"|A|B|C", EnumDisabled:"#0#1#0"}`|
|ComboFilter|지원안함 (편집형 콤보 `ComboEdit` 전용 기능이었고 ComboEdit 미지원 — [Combo,ComboEdit 마이그레이션](/docs/migration/migration-06-03) 참고). 비편집 `Enum` 드롭다운 검색은 [EnumFilter (col)](/docs/props/col/enum-filter) 참고|
|Cursor|[Cursor (col)](/docs/props/col/cursor)로 동일 (열 위 마우스 호버 시 커서 모양, CSS cursor 값: `pointer`/`move`/`text` 등)<br/>ex) `{Type:"Text", Name:"sNm", Cursor:"pointer"}`|
|DefaultValue|[DefaultValue (col)](/docs/props/col/default-value)로 동일 (신규 입력 시 기본값)<br/>ex) `{Type:"Text", Name:"dept", DefaultValue:"미정"}`|
|Edit,EditLen|`Edit`는 [CanEdit (col)](/docs/props/col/can-edit)로 `EditLen`은 [Size (col)](/docs/props/col/size)로 변경되었습니다.|
|EditPointCount|편집 시 소수점 **입력 제한**은 [EditMask (col)](/docs/props/col/edit-mask) 정규식으로 처리<br/>ex) `{Type:"Float", EditMask:"^-?\\d*(\\.\\d{0,2})?$"}`  // 소수점 2자리까지|
|EmptyToReplaceChar|[EmptyValue (col)](/docs/props/col/empty-value)로 변경되었습니다.|
|EnterMode|[AcceptEnters (col)](/docs/props/col/accept-enters)로 변경 (`Lines` 타입 편집 중 Enter 동작, `1`=Enter로 줄넘김 삽입)<br/>ex) `{Type:"Lines", Name:"memo", AcceptEnters:1}`|
|ExcludeEmpty|[ExcludeEmpty (col)](/docs/props/col/exclude-empty)로 동일 (합계·소계의 평균/건수/최소 계산 시 `0`·빈 값 제외 여부, `1`=제외)<br/>ex) `{Type:"Int", Name:"score", ExcludeEmpty:1}`|
|Focus|[CanFocus (col)](/docs/props/col/can-focus)로 변경 (포커스 허용 여부, `0`:포커스 불가)<br/>ex) `{Type:"Text", Name:"sNo", CanFocus:0}`|
|FontBold,FontUnderline|[TextStyle (col)](/docs/props/col/text-style)로 속성명 변경. bold외 밑줄,스트라이크,기울임등을 설정할 수 있습니다.|
|FontColor|[TextColor (col)](/docs/props/col/text-color)로 속성명 변경. 사용법은 동일합니다.|
|FullInput|지원안함 (저장 시 `EditLen` 전체 길이를 입력했는지 체크하던 기능, 대응 없음)|
|HeaderCheck|[HeaderCheck (col)](/docs/props/col/header-check)로 동일 (`Bool` 열 헤더에 전체 체크박스 생성, 클릭 시 일괄 체크/해제). 모든 Bool 열 일괄 적용은 [HeaderCheck (cfg)](/docs/props/cfg/header-check)<br/>ex) `{Type:"Bool", Name:"chk", HeaderCheck:1}`|
|Hidden|[Visible (col)](/docs/props/col/visible)로 변경되었습니다. 따라서 값도 기존과 반대로 입력되어야 합니다.(`Hidden` 속성은 실제 행의 높이 혹은 열의 너비만 줄여서 표시합니다.)|
|ImgWidth,ImgHeight|별도 col 속성이 아니라, `Img` 타입의 **조회 데이터 문자열**에 너비/높이를 포함해 지정합니다. 데이터는 `URL`, `Width`, `Height`, `Left`, `Top`, `LinkUrl`, `Target`, `Background-size`를 **첫 글자 구분자로 이어 붙인** 형식이며, 형식·예시는 [Type](/docs/appx/type)의 `Img` 항목을 참고하세요.|
|InputCaseSensitive|지원안함 (직접 대응 속성 없음). 필요 시 키 이벤트([onKeyUp](/docs/events/on-key-up) 등)로 직접 구현|
|KeyField|[Required (col)](/docs/props/col/required)로 속성명 변경. 사용법은 동일합니다.|
|MaximumValue,MinimumValue|[onEndEdit (event)](/docs/events/on-end-edit)에서 검사하도록 구현해야 합니다. ([예제참고](/docs/migration/migration-06-05))|
|MultiLineText|여러 줄 텍스트 입력 속성. `Lines` 타입(`Type:"Lines"`)으로 변경되었습니다. ([Type](/docs/appx/type) 참고)|
|NumberSort|[NumberSort (col)](/docs/props/col/number-sort)로 동일 (`1`=숫자형, `0`=문자형 정렬)|
|PointCount|소수점 **표시** 자리수는 [Format (col)](/docs/props/col/format)로 처리 (`#,##0.00`=항상 2자리 `12.5`→`12.50`, `#,##0.##`=있을 때만)<br/>ex) `{Type:"Float", Format:"#,##0.00"}`|
|RowMerge|col 속성에서는 지원안함. IBSheet8은 머지를 Cfg에서 처리합니다 — [DataMerge (cfg)](/docs/props/cfg/data-merge), [PrevColumnMerge (cfg)](/docs/props/cfg/prev-column-merge) 등 (위 Cfg 표의 `MergeSheet` 참고)|
|SaveName|[Name (col)](/docs/props/col/name)으로 속성명 변경|
|Sort|[CanSort (col)](/docs/props/col/can-sort)로 속성명 변경. 사용법은 동일합니다.|
|SumType|지원안함. 합계행의 계산 종류는 [FormulaRow (col)](/docs/props/col/formula-row) 값(`Sum`/`Avg`/`Max` 등)으로 대체<br/>ex) `{Type:"Int", Name:"amt", FormulaRow:"Sum"}`|
|ToolTip|[Tip (col)](/docs/props/col/tip)으로 속성명 변경. 사용법은 동일합니다.|
|Transaction|[NoChanged (col)](/docs/props/col/no-changed)로 변경<br/>ex) `{Type:"Text", Name:"memo", NoChanged:1}`|
|TreeCheck|[TreeCheckSync (cfg)](/docs/props/cfg/tree-check-sync)로 변경. [MainCol (cfg)](/docs/props/cfg/main-col) 트리에서 `Icon`/`Button`이 `"Check"`인 컬럼의 **부모/자식 체크 동기화**를 설정합니다 (col 플래그가 아니라 Cfg).<br/>ex) Cfg `{MainCol:"sName", TreeCheckSync:1}` + 체크 컬럼 `{Name:"sName", Icon:"Check"}`|
|TreeCol|[MainCol (cfg)](/docs/props/cfg/main-col)로 변경. 트리 기준이 될 열을 (col 플래그가 아니라) Cfg에 열이름으로 지정<br/>ex) `options.Cfg = {MainCol:"sName"}`|
|TrueValue,FalseValue|[TrueValue (col)](/docs/props/col/true-value), [FalseValue (col)](/docs/props/col/false-value)로 동일. `Bool` 열에서 체크/해제 시 서버와 주고받는 값(예: `"Y"`/`"N"`). 시트 내부는 항상 `1`/`0`으로 처리됨<br/>ex) `{Type:"Bool", Name:"useYn", TrueValue:"Y", FalseValue:"N"}`|
|InsertEdit|[AddEdit(col)](/docs/props/col/add-edit)으로 속성명 변경|
|UpdateEdit|[ChangeEdit(col)](/docs/props/col/change-edit)으로 속성명 변경|
|Validation|지원안함 (IBSheet8 Enum은 편집형이 아님 — 편집형 콤보 관련은 [Combo,ComboEdit 마이그레이션](/docs/migration/migration-06-03) 참고)|
|VAlign|[VAlign (col)](/docs/props/col/v-align)로 동일 (셀 상하 정렬: `Top`/`Middle`/`Bottom`)<br/>ex) `{Type:"Text", Name:"memo", VAlign:"Top"}`|
|Width|기존과 동일합니다.<br/>그리고 [MinWidth (col)](/docs/props/col/min-width), [MaxWidth (col)](/docs/props/col/max-width), [RelWidth (col)](/docs/props/col/rel-width)를 통해 열 너비의 최소,최대 크기나 상대적 크기를 설정하실 수 있습니다.|
|Wrap|[Wrap (col)](/docs/props/col/wrap)로 동일 (셀 내용 줄넘김 → 행 높이 증가, `Lines` 타입은 기본 `1`). `SearchMode` `0`/`3`에서는 [AutoRowHeight (cfg)](/docs/props/cfg/auto-row-height)도 함께 설정<br/>ex) `{Type:"Text", Name:"memo", Wrap:1}`|
|ZeroToReplaceChar|[Format (col)](/docs/props/col/format)의 다중 섹션으로 처리. `;`로 `양수;음수;0` 형식을 지정하면 0일 때 표시할 문자를 따로 줄 수 있습니다<br/>ex) `{Type:"Int", Name:"amt", Format:"#,##0;-#,##0;-"}`  // 값이 0이면 `-` 표시|
