# CustomScroll ***(cfg)***

> 시트에서 사용할 스크롤바의 스타일을 설정합니다.  
> 브라우저 기본 스크롤 또는 IBSheet에서 제공하는 커스텀 스타일을 선택할 수 있습니다.
>
> 데이터 행/열 수가 많은 경우, `CustomScroll` 사용 시 성능 저하가 발생할 수 있습니다.
>
> `SearchMode: 2 (LazyLoad)` 환경에서 조회 데이터가 5만 건 이상이고 IE 브라우저를 사용하는 경우,  
> 브라우저 스크롤 한계로 인해 `0` 이외의 값으로 설정해야 합니다.

<!-- synonyms: custom scroll, scroll bar style, browser scroll, custom scrollbar, 스크롤바 스타일, 커스텀 스크롤 -->

### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`0`|브라우저 기본 스크롤바 사용 (`default`)<br>![CustomScroll0](/assets/imgs/customScroll0.png "CustomScroll0") (by Chrome)|
|`1`|기본 스타일의 커스텀 스크롤바 사용<br>![CustomScroll1](/assets/imgs/customScroll1.png "CustomScroll1") (by Chrome)|
|`2`|큰 스타일의 커스텀 스크롤바 사용<br>![CustomScroll2](/assets/imgs/customScroll2.png "CustomScroll2") (by Chrome)|
|`3`|작은 스타일의 커스텀 스크롤바 사용<br>![CustomScroll3](/assets/imgs/customScroll3.png "CustomScroll3") (by Chrome)|


### Example
```javascript
options.Cfg = {
    CustomScroll: 3      // 작은 스타일의 커스텀 스크롤바 사용
};
```

### Try it
- [Demo of CustomScroll](https://jsfiddle.net/gh/get/library/pure/ibsheet/ibsheet8-manual-sample/tree/master/samples/properties/Cfg/CustomScroll/)

### Read More
- [TouchScroll cfg](./touch-scroll)
- [CustomThumbMinSize cfg](./custom-thumb-min-size)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
