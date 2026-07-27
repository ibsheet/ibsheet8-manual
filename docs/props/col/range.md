# Range ***(col)***

<!-- synonyms: 다중 선택, 복수 선택, 여러개 선택, 한 셀에 체크박스 여러개, 멀티 체크박스, 멀티 셀렉트, range multi select -->

> [Type](/docs/appx/type)이 `Enum`, `Radio`, `File`, `Date`인 열에서 복수 선택 허용 여부를 설정합니다.  
> 복수 선택된 값은 `locale/*.js`의 구분자로 연결됩니다. 모든 타입에서 항목 구분자(`ValueSeparator`)를 쓰고, `Date`는 연속 구간을 추가로 범위 구분자(`RangeSeparator`)로 묶습니다.

### 항목 구분자 (`Enum`, `Radio`, `File`, `Date`)

|구분자|기본값|용도|
|---|---|---|
|`ValueSeparator`|`;`|**데이터 구분자** — 조회 입력(예: `{gift: "A;C"}`)과 저장(`getSaveJson` 등) 시 사용|
|`ValueSeparatorHtml`|`;`|**화면 구분자** — 셀에 표시될 때 사용. 가독성을 위해 `,` 등으로 변경 가능 (예: `,`로 변경 시 셀에 `"갈비세트,사과배"`로 표시)|

### 범위 구분자 (`Date` 전용)

`Date`에서 연속된 날짜는 `시작~끝` 한 덩어리로 묶이고, 그 덩어리들 사이는 위의 `ValueSeparator`로 연결됩니다.  
예: 데이터 `"2026/05/14;2026/05/26~2026/05/28"` → 화면 `"2026/05/14,2026/05/26~2026/05/28"` (ValueSeparatorHtml을 `,`로 변경한 경우)

|구분자|기본값|용도|
|---|---|---|
|`RangeSeparator`|`~`|**데이터 구분자** — 연속 날짜 범위의 시작/끝 사이를 연결|
|`RangeSeparatorHtml`|`~`|**화면 구분자** — 셀에 표시될 때 사용|

### Type별 동작
|Type|`Range:0` (기본)|비교 이미지|`Range:1`|비교 이미지|
|---|---|---|---|---|
|`Enum`|드랍리스트에서 단일 선택|![Enum Range:0](/assets/imgs/range0_enum.png "Enum Range:0")|드랍리스트 내 아이템 옆에 체크박스가 표시되어 여러 개 선택 (체크박스 위치는 [RangeEnumIconLeft cfg](/docs/props/cfg/range-enum-icon-left)로 좌/우 변경)|![Enum Range:1](/assets/imgs/range1_enum.png "Enum Range:1")|
|`Radio`|라디오 버튼으로 단일 선택|![Radio Range:0](/assets/imgs/range0_radio.png "Radio Range:0")|한 셀 안에 체크박스 여러 개가 인라인 표시 (예: `☑A ☐B ☑C ☑D`)|![Radio Range:1](/assets/imgs/range1_radio.png "Radio Range:1")|
|`File`|파일 선택창에서 한 번에 1개 파일만 선택 가능|![File Range:0](/assets/imgs/range0_file.png "File Range:0")|파일 선택창에서 여러 파일을 한 번에 선택 가능 (`<input multiple>` 동작)|![File Range:1](/assets/imgs/range1_file.png "File Range:1")|
|`Date`|달력에서 단일 일자 선택|![Date Range:0](/assets/imgs/range0_date.png "Date Range:0")|달력에서 드래그로 여러 일자 선택. 연속된 날짜는 `시작~끝` 형식으로 묶임 (예: `2026/05/14,2026/05/26~2026/05/28`)|![Date Range:1](/assets/imgs/range1_date.png "Date Range:1")|


### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)` | 단일 선택만 허용 (`default`)|
|`1(true)` | 복수 선택 허용|

### Example
```javascript
// 컬럼 설정
options.Cols = [
    // Enum: 드랍리스트 내에서 여러 아이템 체크 선택
    {Header: "명절선물", Type: "Enum", Name: "gift", Range: 1,
        Enum: "|갈비세트|조기세트|사과배|스팸3호", EnumKeys: "|A|B|C|D"},

    // Radio: 한 셀에 체크박스 여러 개 인라인 표시 (☑A ☐B ☑C ☑D)
    {Header: "선택사항", Type: "Radio", Name: "options", Range: 1,
        Enum: "|A|B|C|D", EnumKeys: "|A|B|C|D"},

    // File: 한 셀에서 여러 파일 업로드/선택
    {Header: "파일선택", Type: "File", Name: "lblist", Range: 1},

    // Date: 달력에서 드래그로 여러 일자 선택
    // Format(화면 표시) / DataFormat(서버 입출력) 함께 지정 권장
    {Header: "기간선택", Type: "Date", Name: "period", Range: 1,
        Format: "yyyy-MM-dd", DataFormat: "yyyyMMdd"}
];

// 조회 데이터 (Range:1 적용 시 각 셀에 들어갈 값 형식)
var data = [
    {
        gift:    "A;C",                          // Enum: 갈비세트, 사과배 선택
        options: "A;C",                          // Radio: A, C 선택

        // File: 파일명과 경로(`{Name}Path`)는 함께 전달해야 셀에 표시됨
        // (Path 없이는 표시 X — Cfg.Export.FilePath로 공통 경로 대체도 가능)
        lblist:     "file1.png;file2.png",       // File: 파일 2개 (ValueSeparator로 연결)
        lblistPath: "/IBSheet/file/",            // File 저장 경로

        period:  "20260514;20260526~20260528"    // Date: 5/14 단일 + 5/26~5/28 범위
    }
];
```

### Read More
- [Enum col](./enum)
- [EnumKeys col](./enum-keys)
- [Radio col](./radio)
- [RangeEnumIconLeft cfg](/docs/props/cfg/range-enum-icon-left)
- [Export cfg (FilePath)](/docs/props/cfg/export)
- [Path cell](/docs/props/cell/path)
- [File Type Upload appendix](/docs/appx/file-type-upload)
- [Type appendix](/docs/appx/type)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
