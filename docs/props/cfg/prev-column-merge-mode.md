# PrevColumnMergeMode ***(cfg)***
> [SearchMode:2](/docs/props/cfg/search-mode)에서 셀을 머지하는 기준을 설정하는 옵션입니다.  
> SearchMode:2는 머지된 모든 Row가 한 Table 안에 그려지기 때문에 머지된 셀이 많은 경우 성능 문제가 발생할 수 있습니다.  
> `PrevColumnMergeMode:1` 설정 시 [PageLength](/docs/props/cfg/page-length)만큼 페이지 단위로 나누어 그려지기 때문에 성능이 향상됩니다. 단, 페이지 경계에서 머지가 끊어집니다.

### 동작 이미지
**`PrevColumnMergeMode:0(default)`**  
![prevColumnMergeMode:0](/assets/imgs/prevColumnMergemode0.png)

**`PrevColumnMergeMode:1, PageLength:10`**  
![prevColumnMergeMode:1](/assets/imgs/prevColumnMergemode1.png)

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`| 같은 값을 가지는 모든 셀을 머지함 (`default`)|
|`1(true)`| 페이지 단위로 나누어 셀을 머지함 |

### Example
```javascript
options = {
    Cfg: {
      PrevColumnMergeMode: 1,  // 페이지 단위로 나누어 셀을 머지합니다.
      ...
    }
};
```

### Read More
- [PrevColumnMerge cfg](./prev-column-merge)
- [SearchMode cfg](/docs/props/cfg/search-mode)
- [DataMerge cfg](/docs/props/cfg/data-merge)
- [PageLength cfg](/docs/props/cfg/page-length)
- [setAutoMerge method](/docs/funcs/core/set-auto-merge)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.11|기능 추가|
|core|8.0.0.12|default 변경 (1 -> 0)|