# 조회 응답 규격 ***(search response structure)***
[SearchMode](/docs/props/cfg/search-mode) 0, 1, 2에서 [doSearch](/docs/funcs/core/do-search) 또는 [loadSearchData](/docs/funcs/core/load-search-data) 함수로 데이터 바인딩 시 사용되는 `조회 응답 규격`의 형식을 정의합니다.

<!--## doSearch나 loadSearchData Method 데이터 규격-->
## 기본 데이터 규격
- `doSearch` 함수 또는 `loadSearchData` 함수에서 데이터 바인딩 시 사용되는 데이터 구조입니다.
- 서버 응답 데이터는 `Data` 속성을 최상위로 가지고 있으며, `Data` 속성 안에는 각각의 항목이 객체 형태로 들어 있는 배열이 포함되어 있습니다.
```js
// Data 속성안에 배열형태로 데이터 구성
{"Data":
    [
        {"sa_name":"홍길동","sa_no":"940154","sa_dept":"A021"},
        {"sa_name":"김지수","sa_no":"950757","sa_dept":"B022"}
    ]
}
```

## 부가 데이터 (etc)
- 조회 응답에 `etc` 속성을 포함하면 시트가 데이터를 받은 후 `sheet.etc`로 접근할 수 있습니다.
- 시트 데이터 외 부가 정보를 함께 전달할 때 사용합니다.
```js
// 응답에 etc 포함
{
    "Data": [
        {"sa_name":"홍길동","sa_no":"940154"},
        {"sa_name":"김지수","sa_no":"950757"}
    ],
    "etc": {
        "total": 1234,
        "pageSize": 50,
        "summary": {"sumPrice": 9999}
    }
}
```
```javascript
// 시트에서 직접 접근
var etcData = sheet.etc;
console.log(etcData.total);   // 1234
```

## 컬럼 Name과 데이터 Key 매핑 규칙 (중요)
- 각 데이터 객체의 key는 **컬럼 정의 시 설정한 `Name` 값과 일치해야 화면에 표시됩니다.**
- `Name` 값과 일치하지 않는 key는 화면에 표시되지 않으며, 대소문자 구분합니다.

```javascript
cols: [
  { Header: "이름", Name: "sa_name" },
  { Header: "사번", Name: "sa_no" }
]
```

위와 같이 정의된 경우:

```json
{
  "Data": [
    {"sa_name":"홍길동","sa_no":"940154"}
  ]
}
```

## Name에 정의되지 않은 Key 사용 가능 여부
- 조회 데이터에 컬럼 `Name`에 정의되지 않은 key를 포함할 수 있습니다.
- 해당 key는 화면에 표시되지 않지만 내부 데이터로 유지됩니다.
- `getValue`,`setValue`, `getRowValue`,`setRowValue`, `getSaveJson` 등의 API를 통해 조회 및 전송에 사용할 수 있습니다.

```js
{
  "Data": [
    {
      "sa_name":"홍길동",
      "sa_no":"940154",
      "row_id":1001,       // 화면에는 표시되지 않음
      "status_flag":"Y"    // 내부 로직용 데이터
    }
  ]
}
```

## 조회 데이터 내에 Row property,Cell property 적용(중요)
- 각 `데이터 행(Row)`에 편집 가능 여부, 색상 등 속성을 지정할 수 있으며, 이 속성을 기준으로 원하는 데이터를 조회할 수 있습니다.
- `데이터 행(Row)`에 적용할 수 있는 속성값은 도움말의 Properties >> Row 에서 확인할 수 있습니다.
```js
// 조회 데이터 안에 Row property에 해당하는 내용을 데이터와 함께 적용
{"Data":
    [
        //1행의 색상을 붉은색으로 표시
        {"sa_name":"홍길동","sa_no":"940154",...      , Color:"#FF8888"},
        //2행을 편집 불가로 설정
        {"sa_name":"김지수","sa_no":"950757",...      , CanEdit:0}
    ]
}
```
- 각 `데이터 셀(Cell)`에 편집 가능 여부, 색상 등 속성을 지정할 수 있으며, 이 속성을 기준으로 원하는 데이터를 조회할 수 있습니다.
- `셀(Cell)`에 적용할 수 있는 속성값은 도움말의 Properties >> Cell 에서 확인할 수 있습니다.
```js
// 조회 데이터 안에 "컬럼명+Cell Property" 형식으로 설정시 Cell 기능 부여
{"Data":
    [
        //1행의  sn_id cell에 글자색 설정
        {"sn_id":"209321","lot":"k0923123",  sn_idTextColor:"#FF0000"},
        //2행의 lot cell에 편집 불가
        {"sn_id":"209327","lot":"r2019283",   lotCanEdit:0},
        //3행의  pos 컬럼(Enum타입)에 item을 해당 셀만 다르게 설정
        {"pos":"A02", posEnum: "|성남시|부천시|광명시|화성시", posEnumKeys: "|A00|A01|A02|A03"}
    ]
}
```
## 조회 데이터  내에 JSON Event 적용
- 각 `데이터 셀(Cell)`에 이벤트를 설정할 수 있으며, 이 속성을 기준으로 원하는 데이터를 조회할 수 있습니다.
- `셀(Cell)`에 적용할 수 있는 이벤트는 도움말의 Properties >> Event 에서 확인할 수 있습니다.
```js
// 조회 데이터에 JSON 이벤트를 포함할수 있습니다.
{"Data":
    [
        //1행의 sa_name컬럼의 값 수정시 sawonPop() 함수 호출
        {"sa_name":"홍길동",sa_nameOnChange:"sawonPop"},
        //2행은 이벤트 없음
        {"sa_name":"홍길동"}
    ],
}
```
서버에서 반환된 조회 데이터는 [onReceiveData](/docs/events/on-receive-data), [onBeforeDataLoad](/docs/events/on-before-data-load), [onDataLoad](/docs/events/on-data-load) 이벤트를 통해 확인할 수 있습니다.

## IBSheet 생성 시 초기 데이터 지정
- 시트 객체 생성시 `data` 영역에 데이터를 지정하면 시트가 그려지면서 데이터가 표시됩니다.
- 조회와 관련된 이벤트는 발생하지 않습니다.

```javascript
//IBSheet.create()에 data 속성을 통해 생성시 데이터 구조
IBSheet.create({
    id:"sheet", // 생성할 시트의 id
    el:"sheetDiv", // 시트를 생성할 Dom 객체 및 id
    options: options, // 생성될 시트의 속성
    // 생성될 시트의 데이터
    data: [
            {"sa_name":"홍길동","sa_no":"940154","sa_dept":"A021"},
            {"sa_name":"김지수","sa_no":"950757","sa_dept":"B022"}
        ]
});
```

## 데이터와 결과 규격
- 서버 응답에 `IO` 속성이 포함된 경우, 조회 처리 과정에서 `onBeforeDataLoad`와 `onDataLoad`이벤트의 파라미터로 `result`와 `message`가 전달됩니다.
- `Result` 값은 조회 `성공/실패` 여부를 판단하는 기준으로 사용되며, `0` 이상의 값은 `정상` 조회, 0보다 작은 `음수` 값은 조회 중 `오류`로 처리됩니다.
- `Message` 값은 `Result`에 대한 설명 메시지입니다.
- 조회 결과가 **정상**(`Result >= 0`)인 경우, 기본적으로 화면에는 표시되지 않습니다.<br/>
  정상 조회 시 메시지를 표시하고 싶으면 `onDataLoad`이벤트 등에서 직접 처리할 수 있습니다.
- 조회 결과가 **에러**(`Result < 0`)인 경우, IBSheet에서 자동으로 에러 메시지를 표시합니다.
```js
// Data 속성안에 배열형태로 데이터 구성
{"Data":
    [
        {"sa_name":"홍길동","sa_no":"940154","sa_dept":"A021"},
        {"sa_name":"김지수","sa_no":"950757","sa_dept":"B022"}
    ],
  "IO": {"Result": 0, "Message": "조회 성공"}
}
```
| Result | Description| Message(ko, en.js)|
| --   | -- |-- |
|  0   |  조회 성공  ||
|  -1  | 빈 URL (예: sheet.doSearch("")) 호출 시  |Url의 값이 없습니다.<br/>(ResultErrEmptyURL)|
|  -3  | 요청 Url이 잘못된 경우나 네트워크 오류 등으로 결과를 받지 못한 경우(404,500등의 에러)  |Url의 값이 잘못됐습니다.<br/>(ResultErrBadURL)|
|  -5  | 응답 결과가 빈 값인 경우  |Url에서 응답이 없습니다.<br/>(ResultErrEmptyResponse)|
|  -6  | 연결 시간 초과((cfg)Timeout 초과) |연결시간이 초과됐습니다.<br/>(ResultErrRequestTimeout)|
|  -7  | 잘못된 데이터 형식(데이터 이상) |데이터 형식이 잘못됐습니다.<br/>(ResultErrBadDataFormat)|
|  그외 | 사용자 정의 코드<br/>`IO`에 정의된 내용을 `onBeforeDataLoad`, `onDataLoad`의 `result`와 `message`파라미터에서 확인가능 ||

### Read More
- [SearchMode cfg](/docs/props/cfg/search-mode)
- [페이징 응답 규격](/docs/dataStructure/paging-structure)
- [doSearch method](/docs/funcs/core/do-search)
- [loadSearchData method](/docs/funcs/core/load-search-data)
- [getChangedData method](/docs/funcs/core/get-changed-data)
- [onReceiveData](/docs/events/on-receive-data)
- [onBeforeDataLoad](/docs/events/on-before-data-load)
- [onDataLoad](/docs/events/on-data-load)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
