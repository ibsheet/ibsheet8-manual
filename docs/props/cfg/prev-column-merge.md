# PrevColumnMerge ***(cfg)***

> 열 기준 병합 시 앞 열의 병합 범위를 기준으로 병합합니다.  
> [DataMerge](/docs/props/cfg/data-merge)와 [HeaderMerge](/docs/props/cfg/header-merge) 옵션이 설정되어 있어야 정상적으로 동작합니다.  
> 시트 생성 후 [setAutoMerge](/docs/funcs/core/set-auto-merge) 메소드를 이용하여 병합을 동적으로 변경할 수 있습니다.  
> 소계([makeSubTotal](/docs/funcs/core/make-sub-total)) 사용 시 `usermerge` 설정에 따라 이 옵션이 무시될 수 있습니다.  
> 자세한 내용은 makeSubTotal의 `usermerge` 파라미터를 참고하세요.

### 동작 이미지
![prevColumnMerge](/assets/imgs/prevColumnMerge_base.png)

[ColMerge](/docs/props/col/col-merge) 값이 0인 컬럼은 탐색 범위에서 제외됩니다. (좌측 컬럼이 ColMerge:0인 경우, 해당 컬럼을 건너뛰고 좌측 컬럼을 기준으로 병합합니다)

![prevColumnMerge](/assets/imgs/prevColumnMerge_colMerge.png)

### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`0`| 전체영역에 앞컬럼 머지기능을 사용안함 (`default`)|
|`1`| 데이터 영역에만 앞컬럼머지기능을 사용|
|`2`| 헤더 영역에서만 앞컬럼머지기능을 사용|
|`3`| 데이터 및 헤더 영역에서 앞컬럼머지 기능 사용|

### Example
```javascript
options = {
    Cfg: {
      DataMerge: 1,        // 열 기준 병합
      PrevColumnMerge: 1   // 앞 열 병합 범위 기준으로 병합
    }
};
```

### Read More
- [HeaderMerge cfg](/docs/props/cfg/header-merge)
- [DataMerge cfg](/docs/props/cfg/data-merge)
- [FixPrevColumnMerge cfg](./fix-prev-column-merge)
- [PrevColumnMergeMode cfg](./prev-column-merge-mode)
- [ColMerge col](/docs/props/col/col-merge)
- [setAutoMerge method](/docs/funcs/core/set-auto-merge)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
