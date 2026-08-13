# MaxVScroll ***(cfg)***

<!-- synonyms: MaxVScroll, max v scroll, max vertical scroll, max height scroll, NoVScroll height limit, 최대 세로 스크롤, 세로 스크롤 최대 높이, 스크롤 생성 높이, NoVScroll 높이, 시트 최대 높이, 스크롤 발생 높이 -->

> `NoVScroll`을 사용할 때, 지정한 높이부터 세로 스크롤이 생기도록 **최대 높이**를 지정하는 기능입니다.  
> **주의**: `MaxVScroll`은 시트 생성 시 el의 높이를 정합니다. 생성 후 이 값을 바꾸면 el 높이가 자동으로 갱신되지 않으므로, el의 높이를 직접 다시 설정해야 합니다.

### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`number`|스크롤이 생기는 최대 높이|

### Example
```javascript
options = {
    Cfg:{
      NoVScroll: 1,
      MaxVScroll: 500
    }
 };
```

### Read More
- [NoVScroll cfg](./no-v-scroll)
- [시트객체 높이 설정 appendix](/docs/appx/sheet-height)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.23|기능 추가|
