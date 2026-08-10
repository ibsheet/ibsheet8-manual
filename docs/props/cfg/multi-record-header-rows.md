# MultiRecordHeaderRows ***(cfg)***

<!-- synonyms: MultiRecordHeaderRows, multi record header rows, multirecord header rows, record header rows, 멀티레코드 헤더행, 멀티레코드 헤더 행 개수, MultiRecord 헤더 행, 헤더 행 개수 조절, 멀티레코드 헤더 수 -->

> 멀티레코드([MultiRecord](/docs/props/cfg/multi-record)) 기능을 사용하는 시트에서 헤더행의 행 개수를 조절하는 기능입니다.  
> 생성된 행 개수보다 많게 설정할 수 없습니다. (단위데이터행 개수가 3개인데 헤더행의 개수는 4개로 설정 할 수 없음)  
> 멀티레코드 레이아웃은 엑셀 다운로드/업로드, `doPrint`, `down2Pdf` 등 출력 시에는 기본적으로 유지되지 않습니다. (`down2Excel`은 [MultiRecordShape](/docs/props/cfg/multi-record-shape):`1`로 화면 모양 그대로 받을 수 있으나 머지가 많으면 느립니다.)

### Type
`number`


### Options
|Value|Description|
|-----|-----|
|`number`|화면에 표시할 멀티레코드 시트의 헤더행 개수|


### Example

헤더 2줄 / 데이터 4줄 구성 예 (헤더를 데이터와 다르게 병합).

```javascript
options.Cfg = { MultiRecord: 1, MultiRecordHeaderRows: 2, MultiRecordDataRows: 4 };

// Cols는 데이터 줄 수(4)에 맞춰 2차원 배열로 구성합니다.
// 단일 헤더는 Header.RecordRowSpan(세로 병합), 그룹 헤더는 Header.RecordColSpan(가로 병합)으로 지정합니다.
options.Cols = [
    // 1) 첫 헤더 줄 + 데이터
    [
        { Header: { Value: "No",   RecordRowSpan: 4 }, Name: "seq",   Type: "Int",  Width: 60 },
        { Header: { Value: "사번", RecordRowSpan: 4 }, Name: "empNo", Type: "Text", Width: 120 },
        { Header: { Value: "성명", RecordRowSpan: 4 }, Name: "empNm", Type: "Text", Width: 120 },
        { Header: { Value: "법적소속", RecordColSpan: 3 }, Name: "contractType", Type: "Text", Width: 120 },
        { Header: { Value: "법적소속" }, Name: "enterYmd",  Type: "Text", Width: 120 },
        { Header: { Value: "법적소속" }, Name: "retireYmd", Type: "Text", Width: 120 },
        { Header: { Value: "작업상태", RecordRowSpan: 4 }, Name: "workStatus", Type: "Text", Width: 120 },
        { Header: { Value: "예수금",   RecordRowSpan: 4 }, Name: "amt1", Type: "Text", Width: 150 }
    ],
    // 2) 둘째 헤더 줄(그룹 아래 세부 헤더) + 데이터
    [
        { Header: "No", Name: "seq2", RecordRowSpan: 2 },
        { Header: { Value: "사번" }, Name: "empNo2", RecordRowSpan: 2 },
        { Header: { Value: "성명" }, Name: "empNm2", RecordRowSpan: 2 },
        { Header: { Value: "계약구분" }, Name: "contractType2", RecordRowSpan: 2 },
        { Header: { Value: "입사일" }, Name: "enterYmd2", RecordRowSpan: 2 },
        { Header: { Value: "종료일" }, Name: "retireYmd2", RecordRowSpan: 2 },
        { Header: { Value: "작업상태" }, Name: "workStatus2", RecordRowSpan: 2 },
        { Header: { Value: "예수금" }, Name: "amt2" }
    ],
    // 3) 셋째 데이터 줄 (헤더는 비움)
    [
        { Header: "No" }, { Header: "" }, { Header: "" }, { Header: "" }, { Header: "" }, { Header: "" }, { Header: "" },
        { Header: "", Name: "amt3" }
    ],
    // 4) 넷째 데이터 줄
    [
        { Header: "", Name: "seq3" }, { Header: "", Name: "empNo3" }, { Header: "", Name: "empNm3" },
        { Header: "", Name: "contractType3" }, { Header: "", Name: "enterYmd3" }, { Header: "", Name: "retireYmd3" },
        { Header: "", Name: "workStatus3" }, { Header: "", Name: "amt4" }
    ]
];
```

![헤더 2줄 / 데이터 4줄 멀티레코드 예제](/assets/imgs/multiRecordHeaderRows.png "MultiRecordHeaderRows 예제")

### Read More

- [MultiRecord cfg](/docs/props/cfg/multi-record)
- [MultiRecordDataRows Cfg](/docs/props/cfg/multi-record-data-rows)
- [MultiRecordShape cfg](/docs/props/cfg/multi-record-shape)

### Since

|product|version|desc|
|---|---|---|
|core|3.0.53|기능 추가|
