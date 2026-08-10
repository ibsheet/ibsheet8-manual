# TouchScrolling ***(cfg)***

<!-- synonyms: TouchScrolling, touch scrolling, mobile touch scroll, body touch scroll, touch scroll enable, 터치 스크롤, 모바일 터치 스크롤, 바디 터치 스크롤, 모바일 시트 스크롤, 터치 스크롤 활성 -->

> 모바일 환경에서 시트 바디 영역 터치 스크롤이 동작할지 여부를 결정합니다. 

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
| `0` | 모바일 환경에서 시트 바디 영역 터치 스크롤이 동작하지 않습니다.|
| `1` | 모바일 환경에서 시트 바디 영역 터치 스크롤이 동작합니다. (`default`)|

### Example
```javascript
options = {
    Cfg :{
        TouchScrolling: 0, // 모바일 환경에서 시트 바디 영역 터치 스크롤을 막습니다.
        ...
    }
};
```

### Read More

### Since

|product|version|desc|
|---|---|---|
|core|8.3.0.38|기능 추가|
