# MsgLocale ***(cfg)***

<!-- synonyms: MsgLocale, msg locale, language prefix, sheet language, i18n locale, message language, 언어 설정, 메시지 언어, 다국어, 로케일, 언어 로케일, IBSMSG, ko en 메시지, locale, ko.js en.js -->

> 시트에서 사용할 언어(메시지 파일) Language Prefix를 설정합니다.  
> 제품과 함께 배포되는 메시지 파일(ko.js,en.js등)안에 메시지 구조는 다음과 같습니다.
```js
IBSMSG.[Language Prefix] = {
  "Lang": {
     // ... 중략 ...
  }
}
```
> 한국어 외에 다른 나라 언어(메시지)를 사용하고자 하실 때는 해당 메시지 파일(js)를 import 하고, 그에 대한 Language Prefix값을 이 속성으로 설정하시면 됩니다.  
> **이 속성을 설정하지 않으면 사용자 브라우저 언어(`navigator.language`)의 언어 코드 첫 글자를 대문자로 한 값을 Language Prefix로 사용합니다. (예: `ja-JP` → `Ja`, `ko-KR` → `Ko`)**  
> 시트가 사용할 메시지(locale) 파일이 import되어 있지 않으면 아래 경고가 표시되므로, 사용할 언어의 메시지 파일을 반드시 import 하세요. (`MsgLocale`을 `"En"`으로 설정했다면 `en.js`)  
> `[IBSheet] Please import locale file. This browser(or ibsheet) default language code is "Ko". Please check your configuration.`



### Type
`string`

### Options
|Value|언어|메시지 파일|
|-----|-----|-----|
|`Ko`|한국어|`ko.js`|
|`En`|영어|`en.js`|
|`Ja`|일본어|`ja.js`|
|`Jp`|일본어|`jp.js`|
|`Zh`|중국어|`zh.js`|
|`Cn`|중국어|`cn.js`|
|그 외|직접 정의|직접 추가한 Prefix/파일도 사용 가능|


### Example
사용할 언어 파일을 import 하고, 시트 옵션에 해당 Prefix를 지정합니다.

```html
<!-- 영문 메시지 import -->
<script src="./common/ibsheet/locale/en.js"></script>
```

```javascript
options.Cfg = {
   "MsgLocale": "En" //영문 메시지 사용
};
```

### Read More
- [getLocale method](/docs/funcs/core/get-locale)
- [setLocale method](/docs/funcs/core/set-locale)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
