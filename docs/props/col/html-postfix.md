# HtmlPostfix ***(col)***

<!-- synonyms: HTML 접미사, 셀 뒤 태그, 뒷문자 HTML, 값 뒤 HTML, 후위 HTML, html postfix, html suffix, cell append html, trailing html -->

> 열의 각 셀의 문자열 뒤에 원하는 `HTML 태그`를 삽입합니다.

### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`string`|원하는 `HTML태그`|


### Example
```javascript
//열의 뒤에 icon 이미지를 추가한다
options.Cols = [
    ...
    {Type: "Text", Name: "sa_nm", HtmlPostfix: '<i class="fas fa-apple-alt"></i>'},
    ...
];
```

### Read More
- [HtmlPrefix col](./html-prefix)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
