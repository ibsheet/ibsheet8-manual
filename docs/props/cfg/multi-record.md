# MultiRecord ***(cfg)***

> 시트에서 한 건의 데이터(레코드)를 여러 줄로 표시하는 기능입니다.  
> 일반적인 시트는 헤더가 여러 줄이더라도 데이터는 조회된 데이터(레코드)마다 하나의 행으로 표현되는데 이를 여러 행으로 표시되도록 하는 기능입니다.  
> 컬럼 정의(`Col`)에 지정한 셀 병합(`RecordRowSpan` / `RecordColSpan`)이 헤더와 데이터에 함께 적용되어, 헤더와 데이터가 같은 형태로 병합됩니다.  
> 헤더만 데이터와 다르게 병합하려면 `RecordHColSpan` / `RecordHColTitle` 또는 `Header.RecordRowSpan` / `Header.RecordColSpan`을 사용합니다. (두 방식은 함께 사용할 수 없습니다.)

기본 시트와 동작은 동일하나, 다음과 같은 기능 제약이 있습니다.

|구분|제약 내용|
|---|---|
|사용 불가 기능|소계, 그룹, 트리, SelectionSummary<br/>필터 다이얼로그(`UseFilterDialog`), 컬럼페이징(`ColPage`)|
|병합|자동 병합(`setAutoMerge` / `setAutoMergeCancel`) 함수 사용 불가<br/>동적 영역 병합(`setMergeRange` / `setMergeCancel`) 함수 사용 불가<br/>병합은 생성 시 `RecordRowSpan` / `RecordColSpan`으로만 지정 (헤더 전용은 `Header.RecordRowSpan` / `Header.RecordColSpan`)|
|열 제어|열 이동 불가<br/>`hideCol` / `showCol` 불가<br/>동적 열 추가/삭제 불가<br/>생성 시 `Visible` 사용 주의(마지막 열 배치 권장)<br/>셀/열 단위 선택/복사 불가(행 단위만 가능)|
|출력|엑셀 다운로드/업로드, 행 복사/붙여넣기, `doPrint`, `down2Pdf` 시<br/>모든 열이 일렬로 처리되어 화면 모양이 유지되지 않음<br/>(`down2Excel`은 [MultiRecordShape](/docs/props/cfg/multi-record-shape):`1`로 화면 모양 유지 가능, 단 머지 많으면 느림)|
|너비|최상단 헤더행 기준으로 Width 적용(그 외 행의 Width/RelWidth 불가)<br/>`RecordColSpan` 더미컬럼은 RelWidth 미동작|
|기타|`Def.Header.SortIcons:1` 사용 불가<br/>`LeftCols` / `RightCols`와 `Type:"Lines"` 병용 불가|

`Header.RecordRowSpan` / `Header.RecordColSpan` 사용 시 제약:

|구분|제약 내용|
|---|---|
|Header Hover|사용 불가 ([HoverScope](/docs/props/cfg/hover-scope):`1`과 같이 동작)|
|Header Sort|사용 불가|
|헤더 병합|데이터와 헤더 별도 병합 지원 (`Header.RecordRowSpan` / `Header.RecordColSpan`)|
|`RecordHColSpan` / `RecordHColTitle`|사용 불가|


### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`0`|멀티레코드 기능 비활성화 (`default`)|
|`1`|멀티레코드 기능 활성화|
<!--! |`2`|멀티레코드 기능 활성화, 헤더를 Object 형태(`Header.RecordRowSpan`, `Header.RecordColSpan`)으로 설정하여 데이터와 별도 병합 기능 지원| !-->


### Example
```javascript
options.Cfg = {
    SearchMode: 2,
    MultiRecord: 1,   // 멀티레코드 전용 시트로 설정
    FitWidth: true
};

// 멀티레코드는 열 정의(Cols)를 2차원 배열로 구성 (각 원소가 한 레코드의 단위데이터행)
options.Cols = [
    // 첫번째 단위데이터행
    [
        { Header: "선택",   Type: "CheckBox", Name: "CHK",           Align: "Center", Width: 60 },
        { Header: "이미지", Type: "Img",      Name: "sProductImage", Align: "Center", Width: 100, RecordRowSpan: 2 },
        { Header: "종류",   Type: "Text",     Name: "sCategory",     Align: "Center", Width: 160 },
        { Header: "특징",   Type: "Lines",    Name: "sSpec",         Align: "Left",   Width: 300, RecordRowSpan: 2, Wrap: 1 },
        { Header: "가격",   Type: "Int",      Name: "sPrice",        Align: "Right",  Width: 120, RecordRowSpan: 2 }
    ],
    // 두번째 단위데이터행 (RecordRowSpan으로 병합된 열은 헤더만 두고 Name 없이 비웁니다)
    [
        { Header: "순번",   Type: "Text", Name: "SEQ",          Align: "Center" },
        { Header: "이미지" },
        { Header: "제품명", Type: "Text", Name: "sProductName", Align: "Center" },
        { Header: "특징" },
        { Header: "가격" }
    ]
];

// 데이터는 일반 시트와 동일하게 레코드당 객체 하나
var data = [
    { CHK: 0, sProductImage: "|/imgs/1.jpg|60|60|||", sCategory: "가전 > TV > LED TV",
      sSpec: "LED TV / 106cm(42인치) / 풀HD / 60Hz 스캔 / HDMI 2개", sPrice: 663000,
      SEQ: 1, sProductName: "LG전자 42LN5400" },
    { CHK: 0, sProductImage: "|/imgs/2.jpg|60|60|||", sCategory: "가전 > TV > LED TV",
      sSpec: "LED TV / 80cm(32인치) / HD / 스포츠모드 / 타임머신 / HDMI 2개", sPrice: 410000,
      SEQ: 2, sProductName: "LG전자 32LB555B" }
];
```

### Read More
- [RecordRowSpan col](/docs/props/col/record-row-span)
- [RecordColSpan col](/docs/props/col/record-col-span)
- [MultiRecordHeaderRows cfg](/docs/props/cfg/multi-record-header-rows)
- [MultiRecordDataRows cfg](/docs/props/cfg/multi-record-data-rows)
- [MultiRecordShape cfg](/docs/props/cfg/multi-record-shape)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.0.0.4|엑셀 업로드/다운로드 다이얼로그 대응|
<!--! |core|8.3.0.52|`2` 옵션 추가| !-->
