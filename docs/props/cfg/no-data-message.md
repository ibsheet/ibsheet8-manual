# NoDataMessage ***(cfg)***

> 빈 데이터로 시트 생성(IBSheet.create의 data인자), 조회 함수를 이용한 조회시 **"조회된 데이터가 없습니다."** 라는 메세지 표시여부를 설정합니다. 

### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`0`|시트 생성, 조회 시 메세지 표시 안함.|
|`1`|시트 생성 시에만 메세지 표시|
|`2`|조회 시에만 메세지 표시 (`default`)|
|`3`|시트 생성, 조회 시 메세지 표시|


### Example
```javascript
options.Cfg = {
  NoDataMessage: 2,  // 조회 함수를 이용한 조회 시에만 메세지 표시
  ...
};
```

표시되는 **문구 자체나 아이콘을 바꾸려면** 다음과 같이 합니다.

- **전체 화면**: 메시지 파일(`locale/ko.js`)의 `Lang.Text.NoSearchData` 값을 수정합니다.
- **특정 화면**: **조회하기 전에** [setMessage](/docs/funcs/core/set-message)로 문구를 설정합니다. (설정한 값은 이후 조회 시 반영됩니다.)
- **아이콘**: `css/default/main.css`의 `.IBNoDataIcon`을 수정합니다.

```javascript
// 특정 화면에서만 문구 변경 — 조회 전에 설정
sheet.setMessage("NoSearchData", "Text", "변경하려는 문구");
sheet.loadSearchData(rtnData); // 이후 조회 시 반영됨
```

### Read More
- [create static](/docs/static/create)
- [NoDataMiddle cfg](/docs/props/cfg/no-data-middle)
- [loadSearch method](/docs/funcs/core/load-search-data)
- [doSearch method](/docs/funcs/core/do-search)
- [doSearchPaging method](/docs/funcs/core/do-search-paging)
- [setMessage method](/docs/funcs/core/set-message)
- [getMessage method](/docs/funcs/core/get-message)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.6|기능 추가|
