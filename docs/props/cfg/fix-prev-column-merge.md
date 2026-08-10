# FixPrevColumnMerge ***(cfg)***

<!-- synonyms: FixPrevColumnMerge, fix prev column merge, fix reference column merge, anchor column merge, base column merge, 기준 열 병합, 기준 컬럼 병합, 앞 컬럼 무시 병합, 병합 기준 열, 열 병합 기준, DataMerge 기준, setAutoMerge -->

> 행 병합(위아래로 병합) 시 지정한 기준 열의 병합 범위를 기준으로 병합하는 기능입니다.  
> 기준 열보다 `Index`가 큰 열에 대해서만 적용됩니다.  
> [DataMerge](/docs/props/cfg/data-merge)와 [HeaderMerge](/docs/props/cfg/header-merge) 옵션이 설정되어 있어야 정상적으로 동작합니다.  
> [PrevColumnMerge](/docs/props/cfg/prev-column-merge)가 선언되어 있어도 이 속성이 우선 적용됩니다.  
> 시트 생성 후 [setAutoMerge](/docs/funcs/core/set-auto-merge) 메소드를 이용하여 병합을 동적으로 변경할 수 있습니다.

### 동작 이미지
**`정책사업` 컬럼으로 설정한 경우, 앞 컬럼과 관계 없이 기준 컬럼 병합 범위를 기준으로 병합**

![fixPrevColumnMerge1](/assets/imgs/fixprevColumnMerge1.png)

![fixPrevColumnMerge2](/assets/imgs/fixprevColumnMerge2.png)

### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`string`|행 병합 시 기준으로 설정할 열의 이름|

### Example
```javascript
options = {
    Cfg: {
      FixPrevColumnMerge : 'sPolicy',  // sPolicy 열의 병합 범위를 기준으로 병합
      ...
    }
};
```

### Read More
- [HeaderMerge cfg](/docs/props/cfg/header-merge)
- [DataMerge cfg](/docs/props/cfg/data-merge)
- [PrevColumnMerge cfg](/docs/props/cfg/prev-column-merge)
- [ColMerge col](/docs/props/col/col-merge)
- [setAutoMerge method](/docs/funcs/core/set-auto-merge)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.15|기능 추가|
