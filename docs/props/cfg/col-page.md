# ColPage ***(cfg)***
> 컬럼 수가 많은 시트에서 성능 향상을 위해 현재 화면에 보이는 컬럼만 동적으로 렌더링할지 여부를 설정합니다.
>
> 기본적으로는 모든 컬럼의 셀(td)을 한 번에 렌더링합니다.  
> 특히 컬럼 수가 많은 경우 세로 스크롤 시 성능 저하가 발생할 수 있습니다.
>
> `ColPage`를 사용하면 가로 스크롤 위치 및 시트 너비에 따라   
> 필요한 컬럼만 렌더링하는 **컬럼 가상 스크롤 방식**으로 동작하여 스크롤 성능을 개선할 수 있습니다.  
> `SearchMode: 0`, `SearchMode: 2` 에서 사용할 수 있습니다.
>
> 렌더링 단위는 [ColPageLength](./col-page-length)로 설정할 수 있습니다.

<!-- synonyms: column paging, virtual column render, column virtualization, colpage, 컬럼 가상 스크롤, 컬럼 페이징, 컬럼 성능 최적화 -->
### 동작 특성
- ColPage는 현재 화면에 보이는 컬럼만 렌더링하는 **컬럼 가상 렌더링 방식**입니다.
- 가로 스크롤 시 새로 노출되는 컬럼 영역이 동적으로 렌더링됩니다.
- 이 과정에서 컬럼이 순차적으로 표시되는 동작이 보일 수 있으며, 이는 성능 최적화를 위한 **정상 동작**입니다.

### 제약 사항

- **Merge 사용 불가**  
  `ColPage`는 화면에 보이는 컬럼만 렌더링합니다.  
  병합 셀은 렌더링되지 않은 컬럼 영역까지 확장될 수 있으므로 구조적으로 지원되지 않습니다.

- **AutoRowHeight 사용 불가**  
  행 높이 자동 계산은 모든 컬럼의 내용을 기준으로 계산됩니다.  
  `ColPage` 사용 시 일부 컬럼만 렌더링되므로 정확한 높이 계산이 불가능합니다.

- **MultiRecord 사용 불가**  
  MultiRecord는 여러 레코드를 하나의 Row 구조로 배치하는 기능입니다.  
  컬럼 단위 가상 렌더링과 구조적으로 충돌하여 함께 사용할 수 없습니다.

### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`0`|동적 컬럼 렌더링 사용 안 함 (`default`)|
|`1`|현재 화면에 보이는 컬럼만 렌더링|

### Example
```javascript
options.Cfg = {
  ColPage: 1 // 컬럼 페이징 기능을 사용합니다. 
};
```

### Read More
- [ColPageLength cfg](./col-page-length)
- [열(Col) 구조에 대한 이해](/docs/start/col)

### Since

|product|version|desc|
|---|---|---|
|core|8.3.0.11|기능 추가|
|core|8.3.0.51|(Cfg) SearchMode:0 기능 대응|