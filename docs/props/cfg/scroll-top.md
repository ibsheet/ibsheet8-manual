# ScrollTop ***(cfg)***

<!-- synonyms: ScrollTop, scroll top, vertical scroll position, vscroll position, scroll y, 세로 스크롤 위치, 수직 스크롤 위치, 시트 위아래 스크롤 위치, 세로 스크롤바 위치, 스크롤 상단 위치 -->

> 시트의 세로 스크롤바 위치를 설정합니다. (단위: `pixel`) 
>
> 스크롤바의 위치값을 0 이상으로 설정하는 경우 이동된 스크롤 바 위치의 데이터가 보여집니다.


### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`number`|세로 스크롤바의 위치 (`단위: pixel`)  (`default: 0`)|


### Example
```javascript
options.Cfg = {
  ScrollTop: 100      // 상단 스크롤의 스크롤바 시작점에서 100px 이동하여 해당 위치의 데이터를 보여줌.
};
```

### Read More
- [ScrollLeft cfg](./scroll-left)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
