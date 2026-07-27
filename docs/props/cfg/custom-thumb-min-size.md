# CustomThumbMinSize ***(cfg)***

> [CustomScroll](./custom-scroll)을 사용하는 경우, 스크롤바에서 현재 위치를 표시하는 **Thumb**(스크롤 핸들)의 최소 크기를 설정합니다.
>
> 조회 데이터가 많아질수록 Thumb 크기는 자동으로 작아지며,  
> `CustomThumbMinSize`를 설정하면 지정한 값(px) 이하로 줄어들지 않도록 제한할 수 있습니다.
>
> 해당 옵션은 가로 및 세로 스크롤바 모두에 적용됩니다.

<!-- synonyms: custom thumb size, scroll thumb size, minimum thumb size, 스크롤 핸들 크기, 스크롤 thumb 최소 크기 -->


###
![CustomThumbMinSize](/assets/imgs/scrollthumb.png "CustomThumbMinSize")<br/>

### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`number`|스크롤바 Thumb의 최소 크기(px 단위)|



### Example
```javascript
options.Cfg = {
    CustomScroll:1,
    CustomThumbMinSize:150, //Thumb가 150px 이하로 줄어들지 않도록 설정
};
```

### Read More
- [TouchScroll cfg](./touch-scroll)
- [CustomScroll cfg](./custom-scroll)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.2|기능 추가|
