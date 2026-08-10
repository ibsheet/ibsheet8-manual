# getColByIndex ***(method)***

<!-- synonyms: getColByIndex, get-col-by-index, 열 조회, 열이름 확인, 인덱스로 열, 열 찾기, 컬럼 이름, 인덱스 열, column, index -->

> 좌측부터 열의 `index`를 기준으로 열이름을 확인합니다.
>
> `index`는 `1`부터 시작합니다.
>
> 해당 함수는 기본적으로 보여지는 열을 기준으로 확인합니다. 
>
> `includeHideCol` 또는 `Cfg: GetColWithHide` 를  설정하여 `Visible` 관계없이 가져옵니다. 
>
> 우선 순위는 `includeHideCol` > `GetColWithHide` 임으로, `GetColWithHide`를 `true`로 설정 하여도 `includeHideCol`을 `false`로 설정시에는 보여지는 열을 기준으로 동작하게 할 수 있습니다


### Syntax
```javascript
string getColByIndex( index, includeHideCol );
```

### Parameters
|Name|Type|Required|Description|
|----------|-----|---|----|
|index|`number`|<span class='required'>필수</span>|열의 `index`
|includeHideCol|`boolean`|<span class='optional'>선택</span>|`true` 설정시 `Col.Visible` 관계없이 인덱스를 추출함.<br>`0(false)`:숨김 열을 계산 대상으로 포함하지 않음 (`default`)<br>`1(true)`:숨김 열도 계산 대상으로 포함|


### Return Value
***string*** : 지정한 위치에 있는 열이름

### Example
```javascript
//3번째 열(1부터 시작함으로)의 열이름을 확인
var fcol = sheet.getColByIndex(3);
```

### Read More
- [getColIndex method](./get-col-index)
- [GetColWithHide cfg](/docs/props/cfg/get-col-with-hide)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.0.0.11|`includeHideCol` 인자 추가|
