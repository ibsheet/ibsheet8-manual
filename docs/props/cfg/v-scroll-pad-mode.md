# VScrollPadMode ***(cfg)***

<!-- synonyms: VScrollPadMode, v scroll pad mode, vscroll padding, vertical scroll pad, header scroll pad, 세로 스크롤 여백, 세로 스크롤 상단 여백, 세로 스크롤 패딩, 헤더 여백 스크롤, V 스크롤 여백 -->

> 세로 스크롤의 상단에 여백을 설정하는 옵션입니다.

### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`0`|아무 여백도 설정하지 않음 (`default`)|
|`1`|[Kind](/docs/appx/kind)가 `Header`인 Head 행만큼 여백을 설정|

### Example
```javascript
options.Cfg = {
    VScrollPadMode: 1
};
```

### Read More
- [Kind appendix](/docs/appx/kind)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
