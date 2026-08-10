# UnescapeHTML ***(col)***

<!-- synonyms: HTML 이스케이프 해제, 특수문자 변환, 엔티티 디코드, HTML 디코딩, unescape html, html decode, entity decode, escape convert -->

> 조회 데이터의 HTML 이스케이프 문자(`&gt;`, `&amp;`, `&lt;`)를 원래 문자(<, &, >)로 변환하는 기능
>
> 적용 대상 컬럼: `Text`, `Lines`
### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|문자 그대로 조회 (`default`)|
|`1(true)`|문자 unescape 처리하여 조회|


### Example
```javascript
// 조회에 들어오는 문자 HTML unescape 처리
options.Cols = [
  ...
  {
    Type: "Text",
    Name: "TextData",
    Width: 110,
    UnescapeHTML: 1
    ...
  },
  ...
];
```

### Read More
- [SaveHTMLChar cfg](/docs/props/cfg/save-html-char)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.24|기능 추가|
