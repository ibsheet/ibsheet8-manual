# RecordColSpan ***(col)***

<!-- synonyms: 컬럼 병합, 열 병합, 가로 병합, 멀티레코드 병합, ColSpan, record col span, column merge, horizontal merge, multi record span -->

> 멀티레코드([MultiRecord](/docs/props/cfg/multi-record)) 기능을 사용하는 시트에서 특정 컬럼을 기준으로 오른쪽으로 합쳐질 열의 개수를 설정합니다.  
> Html Table 객체의 `ColSpan`과 유사합니다.  
> 헤더만 데이터와 다르게 병합하려면 [Header](/docs/props/col/header)를 `object` 형태로 지정하고 `Header.RecordColSpan`으로 오른쪽으로 합쳐질 열 개수를 설정합니다.  
> **<mark>주의</mark> : `RecordColSpan` 설정으로 머지되어 보이지 않는 컬럼은 `Name`을 설정하면 정상 동작하지 않습니다.**


### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`number`|행 내에서 오른쪽으로 합쳐질 열 개수|



### Example
```javascript
options.Cfg = {
    MultiRecord: 1  // 멀티레코드 전용 시트로 설정
    ...
};

// 멀티레코드 기능 사용시 열설정(1차원 배열 -> 2차원 배열)
// 배송지 주소 열은 RecordColSpan:3으로 오른쪽 3열을 가로로 병합
options.Cols = [
    //첫번째 단위데이터행(DataRow)
    [
        {Header: "주문번호", Name: "ordNo", Type: "Text", Width: 100},
        {Header: "상품",     Name: "prod",  Type: "Text", Width: 100},
        {Header: "수량",     Name: "qty",   Type: "Int",  Width: 100},
        {Header: "금액",     Name: "amt",   Type: "Int",  Width: 100}
    ],
    //두번째 단위데이터행(DataRow)
    [
        {Header: "주문자",   Name: "orderer", Type: "Text", Width: 100},
        {Header: "연락처",   Name: "tel",     Type: "Text", Width: 100},
        {Header: "결제수단", Name: "payType", Type: "Text", Width: 100},
        {Header: "주문일",   Name: "ordDate", Type: "Date", Width: 100}
    ],
    //세번째 단위데이터행(DataRow)
    [
        {Header: "주문메모",    Name: "memo",    Type: "Text", Width: 100},
        {Header: "배송지 주소", Name: "address", Type: "Text", Width: 100, RecordColSpan: 3},
        {Header: "배송지 주소", Width: 50},
        {Header: "배송지 주소", Width: 120}
    ]
];
```

![주문 그리드 — 배송지 주소 가로 병합](/assets/imgs/recordColSpan.png "RecordColSpan 예제")

### Read More
- [RecordRowSpan col](/docs/props/col/record-row-span)
- [RecordHColSpan col](/docs/props/col/record-h-col-span)
- [RecordHColTitle col](/docs/props/col/record-h-col-title)
- [MultiRecord cfg](/docs/props/cfg/multi-record)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
