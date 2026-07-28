# ColPageLength ***(cfg)***

> `ColPage` 사용 시 한 번에 렌더링할 열(Col)의 개수를 설정합니다.  
> `ColPage`는 컬럼 가상 렌더링 방식으로 동작하며,  
> 설정한 개수만큼 컬럼을 묶어서 렌더링합니다.

<!-- synonyms: col page length, column page size, virtual column size, 컬럼 렌더링 개수 -->

### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`number`|한 페이지 단위로 렌더링할 컬럼 수 (`default: 10`)|


### Example
```javascript
options = {
  Cfg :{
    SearchMode: 2,      // 0 또는 2 모두 가능
    ColPage: 1,
    ColPageLength: 5,  // 한 번에 렌더링할 컬럼 수
  }
};
```

### Read More
- [ColPage cfg](./col-page)
- [열(Col) 구조에 대한 이해](/docs/start/col)

### Since

|product|version|desc|
|---|---|---|
|core|8.3.0.11|기능 추가|
