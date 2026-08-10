# HtmlPostfix ***(row)***

<!-- synonyms: html postfix, html suffix, append html, html after text, row html postfix, trailing html, HTML 뒤 삽입, HTML 접미사, HTML 뒷 태그, 문자열 뒤 HTML, 후미 HTML, HtmlPostfix 속성 -->

> 행 전체 각 셀의 문자열 뒤에 원하는 HTML 태그를 삽입합니다.
>
> 이 속성은 행에서 사용되는 일은 거의 드물며, 보통 `Col`이나 `Cell`단위로 사용한다.

### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`string`|원하는 Html태그|


### Example
```javascript
//헤더행의 각 셀 타이틀 끝에 특정 Icon을 추가한다
options.Def.Header = {"HtmlPostfix": '<i class="fas fa-apple-alt"></i>'};
```

### Read More
- [HtmlPrefix row](./html-prefix)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
