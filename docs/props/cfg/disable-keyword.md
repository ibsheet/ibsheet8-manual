# DisableKeyWord ***(cfg)***

> 필터행에서 문자열 컬럼 필터에 사용되는 예약어 `;`(OR)와 `,`(AND)의 사용 여부를 설정합니다.  
> `1(true)`로 설정하면 예약어 기능이 비활성화되며, 필터행에 입력된 값을 예약어로 해석하지 않고 **일반 문자열로 처리하여 필터링**합니다. 
>
> 해당 예약어는 메시지 파일에서 정의되며 기본 설정은 다음과 같습니다.

<!-- synonyms: filter operator, filter separator, filter keyword -->

### 필터 예약어
필터에서 사용하는 예약어는 **메시지 파일**(ko.js, en.js 등)에서 정의되며 필요에 따라 변경할 수 있습니다.  
※ `DisableKeyWord` 설정은 **문자열 컬럼 필터에서 사용하는 `;`(OR), `,`(AND) 예약어에만 적용됩니다.**

|Key|기본값|설명|
|---|---|---|
|`ValueSeparator`|`;`|OR 검색 연산자|
|`ValueSeparatorHtml`|`;`|OR 검색 연산자를 화면에 표시할 문자열|
|`ValueAndSeparator`|`,`|AND 검색 연산자|
|`RangeSeparator`|`~`|범위 검색 연산자|
|`RangeSeparatorHtml`|`~`|범위 검색 연산자를 화면에 표시할 문자열|

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|예약어 기능 사용 (`default`)|
|`1(true)`|예약어 기능 사용하지 않음|


### Example
```javascript
// 필터행에서 예약어 `;`(OR), `,`(AND) 사용 비활성화
options.Cfg = {
    DisableKeyWord: 1
};
```

### Read More
- [showFilter cfg](./show-filter)
- [showFilterRow method](/docs/funcs/core/show-filter-row)
- [doFilter method](/docs/funcs/core/do-filter)
- [필터링 기능](/docs/userGuide/filter)

### Since

|product|version|desc|
|---|---|---|
|core|8.1.0.53|기능 추가|
