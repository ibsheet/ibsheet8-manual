# ShowFilter ***(cfg)***

> 시트 생성 시 **헤더행 바로 아래에 필터행(Filter Row)을 추가할지 여부**를 설정합니다.  
> 필터행이 생성되면 각 열에 조건을 입력하여 데이터를 필터링할 수 있습니다.  
>
> 시트 생성 이후 [showFilterRow](/docs/funcs/core/show-filter-row) 메소드를 통해 **동적으로 필터행을 생성할 수 있습니다.**  
> 문자열 컬럼에서 사용하는 예약어(`,`, `;`) 기능은   
> [DisableKeyWord](/docs/props/cfg/disable-keyword) 설정을 통해 비활성화할 수 있습니다.
>
> 필터링으로 숨겨진 행은 내부적으로 [Visible](/docs/props/row/visible):`0(false)` 값이 설정됩니다.  
> 필터링된 데이터만 Excel로 다운로드하려면 다운로드 옵션에서 `downRows:"Visible"` 설정을 사용할 수 있습니다.
>
> 필터행에 입력할 수 있는 **검색 조건의 예시는 다음과 같습니다.**

### 문자열 컬럼 필터
문자열 컬럼에서는 `,`(AND 검색) 또는 `;`(OR 검색)을 사용할 수 있습니다.

|입력값|설명|예시|
|---|---|---|
|`사과;복숭아`|셀 데이터에 **사과 또는 복숭아가 포함된 행을 모두 표시**|![or](/assets/imgs/filterOr.png "or")|
|`사과,복숭아`|셀 데이터에 **사과와 복숭아가 모두 포함된 행만 표시**|![and](/assets/imgs/filterAnd.png "and")|

※ 실제 필터 결과는 선택한 필터 연산자(같음, 포함, 시작 등)에 따라 달라질 수 있습니다.

### 숫자 / 날짜 컬럼 필터
숫자 또는 날짜 컬럼에서는 `~` 기호를 사용하여 **범위 검색**을 할 수 있습니다.  
이 기능은 **필터 연산자 1(같음), 2(같지않음)** 에서만 사용할 수 있습니다.

|입력값|설명|예시|
|---|---|---|
|`20170101~20181231`|2017-01-01 ~ 2018-12-31 범위의 데이터만 표시|![날짜범위](/assets/imgs/filterRange.png "날짜범위")|
|`20170101~20181231;20241031`|2017-01-01 ~ 2018-12-31 범위의 데이터와 2024-10-31 데이터만 표시|![날짜범위;or](/assets/imgs/filterRangeOr.png "날짜범위")|
|`21000~22000`|21000 ~ 22000 범위의 데이터 표시|![숫자범위](/assets/imgs/filterRange1.png "숫자범위")|
|`99000;21000~22000`|99000 데이터와 21000 ~ 22000 범위의 데이터 표시|![숫자범위;or](/assets/imgs/filterRangeOr1.png "숫자범위")|

### 필터 예약어
필터에서 사용하는 구분자는 **메시지 파일**(ko.js, en.js 등)에서 변경할 수 있습니다.

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
|`0(false)`|필터행을 추가하지 않는다. (`default`)|
|`1(true)`|필터행을 추가한다.|


### Example
```javascript
options = {
    Cfg:{
      ShowFilter: true  // 시트 생성 시 필터행을 함께 생성
    }
};
```

### Try it
- [Demo of ShowFilter](https://jsfiddle.net/gh/get/library/pure/ibsheet/ibsheet8-manual-sample/tree/master/samples/properties/Cfg/ShowFilter-true/)

### Read More

- [DisableKeyWord cfg](/docs/props/cfg/disable-keyword)
- [ClearFilterOff cfg](/docs/props/cfg/clear-filter-off) 
- [hideFilterRow method](/docs/funcs/core/hide-filter-row)
- [showFilterRow method](/docs/funcs/core/show-filter-row)
- [doFilter method](/docs/funcs/core/do-filter)
- [clearFilter method](/docs/funcs/core/clear-filter)
- [hasFilter method](/docs/funcs/core/has-filter)
- [HeaderCheckMode cfg](./header-check-mode)
- [exportData method](/docs/funcs/core/export-data)
- [down2Excel method](/docs/funcs/core/down-to-excel)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
