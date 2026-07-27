# PrevHeaderMerge ***(cfg)***

<!-- synonyms: 헤더 머지, 헤더 병합, 이전 행 헤더 머지, 다중 행 헤더, prev header merge, header alignment -->

> 헤더 머지 시 위쪽 헤더 행의 머지 범위를 기준으로 아래쪽 헤더 행의 병합 여부를 설정합니다.  
> [HeaderMerge](/docs/props/cfg/header-merge) 옵션이 설정되어 있어야 정상적으로 동작합니다.  

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|위쪽 헤더 행의 머지 범위를 기준으로 한 헤더 머지를 사용하지 않음 (`default`)|
|`1(true)`|위쪽 헤더 행의 머지 범위를 기준으로 아래쪽 헤더 행을 병합|

### Example
```javascript
options = {
    Cfg: {
      HeaderMerge: 3,      // 헤더 영역 머지 활성화
      PrevHeaderMerge: 1   // 위쪽 헤더 행의 머지 범위를 기준으로 아래쪽 헤더 행을 병합
    }
};
```

### Read More
- [HeaderMerge cfg](./header-merge)

### Since

|product|version|desc|
|---|---|---|
|core|8.3.0.27|기능 추가|
