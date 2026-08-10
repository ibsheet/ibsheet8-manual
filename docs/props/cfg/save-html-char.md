# SaveHTMLChar ***(cfg)***

<!-- synonyms: SaveHTMLChar, save html char, save html character, escape html save, xss protection, doSave html chars, HTML 문자 저장, XSS 방지, HTML 이스케이프, doSave 저장 HTML, NameCode 변환, HTML 특수문자 저장 -->

> `doSave (queryMode: 0)` 저장시 `<, >, &`가 `NameCode`로 변환되지 않고 그대로 저장됩니다.
> **해당 옵션 사용시 xss (Cross-Site Scripting) 문제가 발생할 수 있으므로 사용에 주의 바랍니다.**

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
| `0(false)` | `<, >, &`가 각각 `&lt;`, `&gt;`, `&amp;`로 변환되어 전송 됨 (`default`)|
| `1(true)` | `<, >, &` 문자 그대로 전송됨|

### Example
```javascript
options.Cfg = {
    SaveHTMLChar: 1   // <, >, & 그대로 서버 전송
};

sheet.doSave({url})
```

### Read More
- [doSave method](/docs/funcs/core/do-save)
- [UnescapeHTML col](/docs/props/col/unescape-html)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.22|기능 추가|