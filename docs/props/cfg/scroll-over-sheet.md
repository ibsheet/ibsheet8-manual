# ScrollOverSheet ***(cfg)***

<!-- synonyms: ScrollOverSheet, scroll over sheet, scroll parent after sheet, propagate scroll, parent scroll, 시트 스크롤 부모 이동, 부모 스크롤 연동, 스크롤 상위 전달, 시트 끝 스크롤, 브라우저 스크롤 연동 -->

> 시트와 브라우저에서 세로 스크롤이 있을 때 시트에서 스크롤이 끝난 후, 상위 부모의 스크롤이 동작하도록 하는 기능 

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|기능 사용 안함 (`default`)|
|`1(true)`|세로 스크롤이 끝난 후, 상위 부모의 스크롤이 동작합니다.|


### Example
```javascript
// 시트의 스크롤이 끝난 후, 부모의 스크롤이 동작하도록 기능 사용
options.Cfg = {
    ScrollOverSheet: true
};
```

### Read More

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.18|기능 추가|
