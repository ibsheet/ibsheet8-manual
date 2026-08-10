# GetColWithHide ***(cfg)***

<!-- synonyms: GetColWithHide, get col with hide, col api include hidden, hidden col api, getColIndex hidden, includeHideCol, 숨긴 열 포함, 숨김 열 API, 열 API 숨김 포함, getColIndex 숨김, Col.Visible 무시, 숨김 컬럼 조회 -->

> `getColIndex, getColByIndex, getFirstCol, getLastCol, getNextCol, getPrevCol` 해당 API들은 기본 기능이 보여지는 열을 기준으로 동작합니다. 
>
> 해당 기능을 `true`로 설정시, 위의 `API`들은 `Col.Visible` 관계없이 동작합니다. 
>
> 우선 순위는 `includeHideCol` > `GetColWithHide` 임으로, `GetColWithHide`를 `true`로 설정 하여도 `includeHideCol`을 `false`로 설정시에는 보여지는 열을 기준으로 동작하게 할 수 있습니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|기능 사용 안함 (`default`)|
|`1(true)`|`getColIndex, getColByIndex, getFirstCol, getLastCol, getNextCol, getPrevCol`- `Col.Visible` 상관없이 동작.|


### Example
```javascript
//getColIndex, getColByIndex, getFirstCol, getLastCol, getNextCol, getPrevCol 해당 API들의 기능을 Visible 관계 없이 동작하도록 합니다.
options.Cfg = {
    GetColWithHide: true
};
```

### Read More
- [getColIndex method](/docs/funcs/core/get-col-index)
- [getColByIndex method](/docs/funcs/core/get-col-by-index)
- [getFirstCol method](/docs/funcs/core/get-first-col)
- [getLastCol method](/docs/funcs/core/get-last-col)
- [getNextCol method](/docs/funcs/core/get-next-col)
- [getPrevCol method](/docs/funcs/core/get-prev-col)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.11|기능 추가|
