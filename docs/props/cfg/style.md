# Style ***(cfg)***

<!-- synonyms: Style, sheet theme, sheet style prefix, css theme, 테마, 시트 테마, 시트 스타일, CSS 테마 prefix, 스타일 prefix, 커스텀 테마, 테마 지정 -->

> `기본 테마(/css/default/main.css)`외에 다른 테마를 적용하고자 할때, 사용할 테마에 정의한 `Prefix` 값을 설정합니다.
>
> 해당 기능을 사용하기 위해서는 사용하고자 하는 css 파일이 화면에 `include` 되어 있어야 합니다.
### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`string`|사용하는 css 파일에 정의한 `Prefix 명`|

**기본으로 제공하는 테마**

|value|Prefix|Description|
|---|---|---|
|`default` 폴더|`IB`(`default`)|시트에서 사용하는 이미지를 svg 제공|
|`default_img` 폴더|`IB`|시트에서 사용하는 이미지를 png, gif 제공|
|`grace` 폴더|`IBGR`|시트에서 사용하는 이미지를 svg 제공|
|`gray` 폴더|`IBGY`|시트에서 사용하는 이미지를 svg 제공|
|`material` 폴더|`IBMR`|시트에서 사용하는 이미지를 svg 제공|
|`mint` 폴더|`IBMT`|시트에서 사용하는 이미지를 svg 제공|
|`simple` 폴더|`IBSP`|시트에서 사용하는 이미지를 svg 제공|
|`krds` 폴더|`IBKD`|시트에서 사용하는 이미지를 svg 제공|


### Example
```javascript
options = {
  Cfg: {
      //사용할 테마 prefix명
      Style: "IBMT",
      ...
  }
};
```

### Read More
- [setTheme method](/docs/funcs/core/set-theme)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
