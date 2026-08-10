# HtmlPrefix ***(row)***

<!-- synonyms: html prefix, prepend html, html before text, row html prefix, leading html, HTML 앞 삽입, HTML 접두사, HTML 앞 태그, 문자열 앞 HTML, 선두 HTML, HtmlPrefix 속성 -->

> 행 전체 각 셀의 문자열 앞에 원하는 HTML 태그를 삽입합니다.
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
//헤더행의 각 셀에 특정 Icon을 추가한다
options.Def.Header = {"HtmlPrefix": '<i class="far fa-angry"></i>'};
```

### Read More
- [HtmlPostfix row](./html-postfix)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
