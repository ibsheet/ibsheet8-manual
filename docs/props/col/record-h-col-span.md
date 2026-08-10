# RecordHColSpan ***(col)***

<!-- synonyms: 헤더 그룹 병합, 상위 헤더, 가로 헤더 병합, 헤더 ColSpan, record h col span, header group span, header column merge -->

> 멀티레코드([MultiRecord](/docs/props/cfg/multi-record)) 시트에서 헤더에 상위 그룹 헤더를 만들어 여러 열을 가로로 묶는 기능입니다.  
> 기준 열에서 오른쪽으로 묶을 열 개수를 지정하고, 그룹 제목은 [RecordHColTitle](/docs/props/col/record-h-col-title)로 붙입니다.   
> 헤더에만 그룹 단계가 추가되며, 각 열의 데이터는 그대로 표시됩니다([RecordRowSpan](/docs/props/col/record-row-span)으로 세로 병합된 열은 레코드당 한 셀로 보임).  
> `RecordRowSpan`이 2 이상이고 [RecordColSpan](/docs/props/col/record-col-span)을 쓰지 않을 때 사용합니다.  
> Html Table 객체의 `ColSpan`과 유사합니다.  
> **주의**  
> - `Header.RecordRowSpan` / `Header.RecordColSpan`을 이용한 헤더 병합과 함께 사용할 수 없습니다.  
> - 해당 컬럼(또는 같은 위치의 상단 단위데이터행 컬럼)에 `Name`이 반드시 선언되어 있어야 합니다.
<!--! > **<mark>주의</mark> : [MultiRecord](/docs/props/cfg/multi-record)를 `2`로 설정하였을 때, 해당 속성은 사용할 수 없습니다.** !-->


### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`number`|헤더 행 내에서 오른쪽으로 합쳐질 열 개수|



### Example
```javascript
options.Cfg = {
   MultiRecord: 1  // 멀티레코드 전용 시트로 설정
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
- [RecordHColTitle col](/docs/props/col/record-h-col-title)
- [RecordRowSpan col](/docs/props/col/record-row-span)
- [RecordColSpan col](/docs/props/col/record-col-span)
- [MultiRecordHeaderRows cfg](/docs/props/cfg/multi-record-header-rows)
- [MultiRecord cfg](/docs/props/cfg/multi-record)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
