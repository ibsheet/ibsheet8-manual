# DataMerge ***(cfg)***
> 조회된 데이터 영역에서 값이 같은 셀을 기준으로 병합할지 여부 및 병합 종류를 설정합니다.  
> 동일한 값이 연속으로 존재하는 경우 설정된 방식에 따라 셀이 자동 병합됩니다.  
> - **열 기준 병합** : 같은 값을 가진 셀이 위/아래 방향으로 병합됩니다.  
> - **행 기준 병합** : 같은 값을 가진 셀이 좌/우 방향으로 병합됩니다.  
> 시트 생성 후 [setAutoMerge](/docs/funcs/core/set-auto-merge) 메소드를 이용하여 병합을 동적으로 변경할 수 있습니다.  
> 소계([makeSubTotal](/docs/funcs/core/make-sub-total)) 사용 시 `usermerge` 설정에 따라 이 옵션이 무시될 수 있습니다. 
> 자세한 내용은 makeSubTotal의 `usermerge` 파라미터를 참고하세요.

<!-- synonyms: data merge, auto merge, cell merge, 자동 병합, 값 기준 병합, 열 병합, 행 병합 -->

### 참고

**병합 적용 조건**
- 열 기준 병합은 [Col.ColMerge](/docs/props/col/col-merge)가 `1`인 컬럼에 적용됩니다.
- 행 기준 병합은 [Row.RowMerge](/docs/props/row/row-merge)가 `1`인 행에 적용됩니다.

**병합 제외 방법**
- 특정 열을 병합에서 제외하려면 해당 컬럼의 `ColMerge`를 `0`으로 설정합니다.
- 특정 행을 병합에서 제외하려면 해당 행의 `RowMerge`를 `0`으로 설정합니다.

**병합 제한**
- `DataMerge`가 설정된 경우 `Span` 및 `RowSpan`은 적용되지 않습니다.
- 트리 구조에서는 `DataMerge: 1`만 지원되며 동일한 레벨(depth) 내에서만 병합됩니다.

### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`0`|병합 안함 (`default`)<br/>![option0](/assets/imgs/dataMerge0.png "option0")|
|`1`|열 기준 병합<br/>![option1](/assets/imgs/dataMerge1.png "option1")|
|`2`|행 기준 병합<br/>![option2](/assets/imgs/dataMerge2.png "option2")|
|`3`|열 기준 병합 후 행 기준 병합 수행<br/>![option3](/assets/imgs/dataMerge3.png "option3")|
|`4`|행 기준 병합 후 열 기준 병합 수행<br/>![option4](/assets/imgs/dataMerge4.png "option4")|
|`5`|열 기준 사방 병합<br/>![option5](/assets/imgs/dataMerge5.png "option5")|
|`6`|행 기준 사방 병합<br/>![option6](/assets/imgs/dataMerge6.png "option6")|


### Example
```javascript
options = {
    "Cfg" :{
      "DataMerge":1,  // 조회된 데이터 영역에서 열 기준 자동 병합
    }
};
```

### Read More
- [ColMerge col](/docs/props/col/col-merge)
- [RowMerge row](/docs/props/row/row-merge)
- [HeaderMerge cfg](./header-merge)
- [PrevColumnMerge cfg](./prev-column-merge)
- [FixPrevColumnMerge cfg](./fix-prev-column-merge)
- [CalcMergeMode cfg](./calc-merge-mode)
- [EditAutoMerge cfg](./edit-auto-merge)
- [MergeCellsMatch cfg](./merge-cells-match)
- [setAutoMerge method](/docs/funcs/core/set-auto-merge)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.0.0.8|트리 구조에서 `DataMerge: 1`만 지원하도록 추가|
