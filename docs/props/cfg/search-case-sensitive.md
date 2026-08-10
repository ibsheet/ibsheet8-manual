# SearchCaseSensitive ***(cfg)***

<!-- synonyms: SearchCaseSensitive, search case sensitive, case sensitive search, search uppercase lowercase, 대소문자 구분 검색, 검색 대소문자, 검색 case sensitive, 대소문자 구별 검색, 영문 검색 대소문자 -->

> 검색어가 영문(혹은 대/소문자를 구분하는 언어)에서 대/소문자를 구분해서 검색하도록 설정할 수 있습니다.
>
> 기본값은 `0(false)`입니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|검색 시 대/소문자를 구분하지 않습니다.(`defalut`)|
|`1(true)`|검색 시 대/소문자를 구분합니다.|


### Example
```javascript
options.Cfg = {
    SearchCaseSensitive: true       // 검색 기능 사용시 영문의 대/소문자 구분해서 검색
};
```

### Read More
- [SearchCount cfg](./search-count)
- [SearchExpression cfg](./search-expression)
- [findRows method](/docs/funcs/core/find-rows)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
