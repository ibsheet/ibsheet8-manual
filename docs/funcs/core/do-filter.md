# doFilter ***(method)***

<!-- synonyms: 필터 실행, 필터링, 필터 적용, 데이터 걸러내기, 필터 수행, 필터행 적용, do-filter, doFilter, do filter, apply filter, filter data, execute filter -->

> 주어진 값을 필터행에 반영하여 시트를 필터링합니다.  
> 이 함수는 반드시 `Cfg.ShowFilter` 설정으로 **필터행이 표시된 상태에서만 사용할 수 있습니다.**
>
> 필터 값의 입력 방식 및 예약어(`,`, `;`, `~`)에 대한 자세한 설명은 [ShowFilter](/docs/props/cfg/show-filter) 문서를 참고하세요.

### Syntax
```javascript
void doFilter( cols , vals , operators , nofilter , noclear );
```

### Parameters
|Name|Type|Required|Description|
|----------|-----|---|----|
|cols|`string`|<span class='required'>필수</span>|필터링을 수행할 열 이름들<br/>첫 글자를 구분자로 사용하여 열 이름을 연결한 문자열 (ex: `"\|DEPTNM\|POSITION\|SALARY"` )|
|vals|`string`|<span class='required'>필수</span>|필터링 값<br/>첫 글자를 구분자로 사용하여 필터 값을 연결한 문자열 (ex: `"\|총무\|대리\|3500"` )|
|operators|`string`|<span class='required'>필수</span>|필터 연산자 값<br/>첫 글자를 구분자로 사용하여 연산자 값을 연결한 문자열 (ex: `"\|11\|11\|3"` )|
|nofilter|`boolean`|<span class='optional'>선택</span>|실제 필터링을 수행하지 않고 필터행에 값만 입력할지 여부<br/>`0(false)`: 필터링 실행 (`default`)<br/>`1(true)`: 필터행에 값만 입력|
|noclear|`boolean`|<span class='optional'>선택</span>|`cols`에서 지정하지 않은 열의 필터 값을 유지할지 여부<br/>`0(false)`: 다른 열의 필터 값 삭제 (`default`)<br/>`1(true)`: 다른 열의 필터 값 유지|



### Filter Operator 값

|value|type|desc|
|---|---|---|
|`0`|공통|사용 안함|
|`1`|공통|같다|
|`2`|공통|같지 않다|
|`3`|숫자, 날짜|작다|
|`4`|숫자, 날짜|작거나 같다|
|`5`|숫자, 날짜|크다|
|`6`|숫자, 날짜|크거나 같다|
|`7`|문자|앞글자 일치|
|`8`|문자|앞글자 일치하지 않음|
|`9`|문자|뒷글자 일치|
|`10`|문자|뒷글자 일치하지 않음|
|`11`|문자|해당 글자 포함|
|`12`|문자|해당 글자 포함하지 않음|
|`13`|숫자|상위 10|
|`14`|공통|값 있음|
|`15`|공통|값 없음|

### Return Value
***none***

### Example
```javascript

// country 열의 데이터가 "한국" 또는 "일본"이 포함되고 amount 열의 값이 10000 ~ 20000 범위인 행만 표시
sheet.doFilter("|country|amount", "|한국;일본|10000~20000", "|11|1");

//기존 필터 조건을 유지한 상태에서 orderDate 열에 "20240115" 조건 추가
sheet.doFilter("|orderDate", "|20240115", "|1",0,1);

```
### Try it
- [Demo of ShowFilter](https://jsfiddle.net/gh/get/library/pure/ibsheet/ibsheet8-manual-sample/tree/master/samples/properties/Cfg/ShowFilter-true/)

### Read More
- [clearFilter method](./clear-filter)
- [hasFilter method](./has-filter)
- [showFilterRow method](./show-filter-row)
- [setFilter method](./set-filter)
- [ShowFilter cfg](/docs/props/cfg/show-filter)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.0.0.27|필터연산자 13 추가|
|core|8.1.0.27|필터연산자 14,15 추가|
