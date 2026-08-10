# ScrollLeft ***(cfg)***

<!-- synonyms: ScrollLeft, scroll left, horizontal scroll position, hscroll position, scroll x, 가로 스크롤 위치, 수평 스크롤 위치, 시트 좌우 스크롤 위치, 스크롤 좌표, 스크롤바 좌측 위치 -->

> 중앙 열 섹션 (일반적인 Cols 영역) 의 가로 스크롤이 생성되는 시트에서 
>
> 가로 스크롤의 스크롤바 위치를 좌측 기준으로 얼마만큼 이동하여 보여줄지를 설정합니다. (`단위: pixel`) 
>
> 스크롤 위치값을 0 이상으로 설정하는 경우 가로 스크롤 바가 이동하여 해당 위치의 데이터가 보여집니다.


### Type
`number`

### Options
|Value|Description|
|-----|-----|
|number|세로 스크롤의 위치 (`단위: pixel`)  (`default: 0`)|


### Example
```javascript
options.Cfg = {
  ScrollLeft: 50      // 세로 스크롤의 시작점에서 스크롤바가 50px 이동하여 해당 위치의 데이터를 보여줌.
};
```

### Read More
- [ScrollTop cfg](./scroll-top)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
