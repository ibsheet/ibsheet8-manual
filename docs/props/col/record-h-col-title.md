# RecordHColTitle ***(col)***

<!-- synonyms: 헤더 그룹 제목, 상위 헤더 제목, 병합 헤더 텍스트, 헤더 라벨, record h col title, header group title, merged header label, upper header text -->

> 멀티레코드([MultiRecord](/docs/props/cfg/multi-record)) 기능을 사용하는 시트에서 [RecordHColSpan](/docs/props/col/record-h-col-span)이 설정 되어 있는 헤더의 열의 제목을 설정합니다.  
> **데이터와 상관없이 동작하며 서버로 전송되지 않습니다.**
<!--! > **<mark>주의</mark> : [MultiRecord](/docs/props/cfg/multi-record)를 `2`로 설정하였을 때, 해당 속성은 사용할 수 없습니다.** !-->



### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`string`|[RecordHColSpan](/docs/props/col/record-h-col-span)이 설정 되어 있는 헤더의 열의 제목|



### Example
```javascript
options.Cfg = {
   MultiRecord: 1 // 멀티레코드 전용 시트로 설정
   ...
};

// 멀티레코드 기능 사용시 열설정(1차원 배열 -> 2차원 배열)
Cols: [
   //첫번째 단위데이터행(DataRow)
   [
      { "Header": "본사", Name: "HeadOffice", "Width": 60, RecordRowSpan: 3, RecordHColSpan: 5, RecordHColTitle: "기관" },
      { "Header": "연구소", Name: "Laboratory", "Width": 60, RecordRowSpan: 3 },
      { "Header": "지사1", Name: "BranchOffice1", "Width": 60, RecordRowSpan: 3 },
      { "Header": "지사2", Name: "BranchOffice2", "Width": 60, RecordRowSpan: 3 },
      { "Header": "기타", Name: "sEtc", "Width": 60, RecordRowSpan: 3 }
   ],

   //두번째 단위데이터행(DataRow)
   [
      { "Header": "본사", RecordHColSpan: 2, RecordHColTitle: "계열1" },
      { "Header": "연구소" },
      { "Header": "지사1", RecordHColSpan: 2, RecordHColTitle: "계열2" },
      { "Header": "지사2" },
      { "Header": "기타" }
   ],

   //세번째 단위데이터행(DataRow)
   [
      { "Header": "본사" },
      { "Header": "연구소" },
      { "Header": "지사1" },
      { "Header": "지사2" },
      { "Header": "기타" }
   ]
];
```

### Read More
- [RecordHColSpan col](/docs/props/col/record-h-col-span)
- [RecordRowSpan col](/docs/props/col/record-row-span)
- [RecordColSpan col](/docs/props/col/record-col-span)
- [MultiRecordHeaderRows cfg](/docs/props/cfg/multi-record-header-rows)
- [MultiRecord cfg](/docs/props/cfg/multi-record)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
