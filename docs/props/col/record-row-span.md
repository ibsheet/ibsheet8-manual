# RecordRowSpan ***(col)***
> 멀티레코드([MultiRecord](/docs/props/cfg/multi-record)) 기능을 사용하는 시트에서 특정 행을 기준으로 아래쪽으로 합쳐질 행의 개수를 설정합니다.  
> Html Table 객체의 `RowSpan`과 유사합니다.  
> 헤더만 데이터와 다르게 병합하려면 [Header](/docs/props/col/header)를 `object` 형태로 지정하고 `Header.RecordRowSpan`으로 아래쪽으로 합쳐질 행 개수를 설정합니다.  
> **<mark>주의</mark> : `RecordRowSpan` 설정으로 머지되어 보이지 않는 컬럼은 `Name`을 설정하면 정상 동작하지 않습니다.**



### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`number`|열 내에서 아래로 병합할 행의 개수|



### Example
```javascript
options.Cfg = {
   MultiRecord: 1  // 멀티레코드 전용 시트로 설정
   ...
};

// 멀티레코드 기능 사용시 열설정(1차원 배열 -> 2차원 배열)
// 사진 열은 RecordRowSpan:3으로 세 데이터행을 세로로 병합
options.Cols = [
    //첫번째 단위데이터행(DataRow)
    [
        {Header: "상품코드", Name: "prodCode", Type: "Text", Width: 100},
        {Header: "사진",     Name: "photo",    Type: "Img",  Width: 100, RecordRowSpan: 3},
        {Header: "가격",     Name: "price",    Type: "Int",  Width: 100},
        {Header: "재고",     Name: "stock",    Type: "Int",  Width: 100}
    ],
    //두번째 단위데이터행(DataRow) — 사진은 위에서 병합했으므로 헤더만 두고 비움
    [
        {Header: "카테고리", Name: "category", Type: "Text", Width: 100},
        {Header: "사진"},
        {Header: "색상",     Name: "color",    Type: "Text", Width: 100},
        {Header: "등록일",   Name: "regDate",  Type: "Date", Width: 100}
    ],
    //세번째 단위데이터행(DataRow)
    [
        {Header: "브랜드", Name: "brand",  Type: "Text", Width: 100},
        {Header: "사진"},
        {Header: "원산지", Name: "origin", Type: "Text", Width: 100},
        {Header: "비고",   Name: "note",   Type: "Text", Width: 100}
    ]
];
```

![상품 그리드 — 사진 열 세로 병합](/assets/imgs/recordRowSpan.png "RecordRowSpan 예제")

### Read More
- [RecordColSpan col](/docs/props/col/record-col-span)
- [RecordHColSpan col](/docs/props/col/record-h-col-span)
- [RecordHColTitle col](/docs/props/col/record-h-col-title)
- [MultiRecord cfg](/docs/props/cfg/multi-record)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
