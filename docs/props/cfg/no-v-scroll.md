# NoVScroll ***(cfg)***

<!-- synonyms: NoVScroll, no v scroll, no vertical scroll, remove vscroll, dynamic height, auto height, 세로 스크롤 없음, 세로 스크롤 안함, V 스크롤 제거, 시트 높이 자동, 세로 스크롤바 제거, 데이터 수 만큼 높이 -->

> 시트에 세로스크롤바를 표시하지 않는 기능으로 조회된 데이터의 갯수만큼 시트의 높이가 동적으로 변경됩니다.
>
> `SearchMode: 1`이나 `SearchMode: 4,5`를 이용한 페이징 조회시에는, 전체 데이터에서 `PageLength`에 설정한 크기만큼 높이가 변경됩니다.
>
> 해당 기능은 `SearchMode: 0`에서는 사용할 수 없습니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|시트내 세로 스크롤 사용 (`default`)|
|`1(true)`|세로 스크롤 사용안함|


### Example
```javascript
options = {
    Cfg:{
      NoVScroll: true  //시트에 세로스크롤바를 표시하지 않고 전체 데이터 양에 따라 높이 자동 조절
    }
};
```

### Read More
- [NoHScroll cfg](./no-h-scroll)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
