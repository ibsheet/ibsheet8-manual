# HeaderSortMode ***(cfg)***

> 헤더를 클릭시 소팅하는 순서를 변경합니다.  
> 별다른 설정이 없는 경우 시트는 [MaxSort](/docs/props/cfg/max-sort) 설정에 따라 클릭하는 헤더의 순서대로, 대분류, 중분류, 소분류로 소팅을 합니다.  
> 가령 `MaxSort:3` 이고 A, B, C 컬럼의 헤더를 순서대로 클릭하였다면 **대분류:A, 중분류:B, 소분류:C**의 순서대로 소팅이 이루어지고 이렇게 3개 컬럼이 결정되고 난 이후에는 다른 컬럼은 클릭하여도 소팅이 되지 않습니다.  
> 그런데 이러한 방식 대신에 마지막으로 클릭한 컬럼을 대분류로 하고, 소팅 컬럼이 결정된 이후에 새롭게 클릭하는 헤더를 계속적으로 대분류로 변경하여 소팅하고자 하실때는 이 속성을 `1`로 설정하시면 됩니다.  
> 만약 기존에 소팅된 내용을 clear하려면 헤더를 `Shift + 클릭` 하시면 됩니다.

### Type
`number`

### Options
|Value|Description|
|-----|-----|
| `0` | 클릭한 순서대로 대분류/중분류/소분류가 되며, `MaxSort`에서 지정한 개수까지만 소팅하고 `MaxSort` 초과의 컬럼은 소팅이 되지 않음. (`default`) |
| `1` | 클릭한 순서의 역순으로 대분류/중분류/소분류가 되며, 마지막으로 클릭하는 헤더가 대분류가 됨. `MaxSort` 초과 시 기존의 소분류였던 컬럼은 소팅 취소됨.|
| `2` | 클릭한 헤더의 소팅 아이콘만 변경되고 실제 소팅이 되지 않음.<br/>단, 헤더 클릭 시점의 정렬만 막을 뿐, 데이터를 다시 조회하면 헤더에 걸린 Sort 기준으로 자동 재정렬됨.|
| `3` | 클릭한 헤더의 소팅 아이콘만 변경되고 실제 소팅이 되지 않음. 추가적으로 [doSort](/docs/funcs/core/do-sort) 이용한 정렬이나 조회 시 자동 재정렬도 되지 않음.<br/>IBSheet 자체 정렬 대신 서버(DB) 정렬을 사용해 조회된 순서를 그대로 표시할 때 이 모드를 사용.|
| `4` | 클릭한 순서대로 대분류/중분류/소분류가 되며, 마지막으로 클릭하는 헤더가 소분류가 됨. `MaxSort` 초과 시 기존의 대분류였던 컬럼은 소팅 취소됨. |

`MaxSort:3`(우선순위 슬롯 3칸)에서 헤더를 `A` → `B` → `C` → `D` 순서로 클릭하면, 모드별로 슬롯이 다음과 같이 채워지고 밀려납니다.

```
우선순위 슬롯: [1순위][2순위][3순위]

mode 0 : 순서대로 채우고, 꽉 차면 새 클릭 무시
  A →  [A][ ][ ]
  B →  [A][B][ ]
  C →  [A][B][C]
  D →  [A][B][C]   ← 꽉 참, D 무시

mode 1 : 새 클릭을 항상 1순위로 넣고 나머지를 밀어냄
  A →  [A][ ][ ]
  B →  [B][A][ ]
  C →  [C][B][A]
  D →  [D][C][B]   ← 넘친 A 탈락

mode 4 : 순서대로 채우다 꽉 차면 1순위를 버리고 새 클릭을 꼴찌로
  A →  [A][ ][ ]
  B →  [A][B][ ]
  C →  [A][B][C]
  D →  [B][C][D]   ← A 탈락, D가 3순위
```

### Example
```javascript
options = {
    Cfg :{
        HeaderSortMode: 1,
        ...
    }
};
```

### Read More
- [MaxSort cfg](/docs/props/cfg/max-sort)
- [HeaderSortActionMode cfg](/docs/props/cfg/header-sort-action-mode)
- [UseHeaderSortCancel cfg](/docs/props/cfg/use-header-sort-cancel)
- [doSort method](/docs/funcs/core/do-sort)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.4|기능 추가|
|core|8.0.0.8|`HeaderSortMode: 2,3` 추가|
|core|8.3.0.43|`HeaderSortMode: 4` 추가|