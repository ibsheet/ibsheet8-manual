# SelectCheck ***(col)***

<!-- synonyms: 드래그 체크, 영역 체크, 일괄 체크, 범위 체크, drag check -->

> `Bool` 타입 컬럼에서 영역을 드래그하여 한 번에 여러 셀의 체크 상태를 토글합니다. (체크 → 체크해제, 체크해제 → 체크)  
> 하나씩 클릭하는 대신 드래그로 일괄 체크/체크해제할 때 유용합니다.  
> `SelectCheck`가 설정된 컬럼에서 드래그가 시작되고 끝나야 동작하며, 머지된 컬럼이나 [SearchMode](/docs/props/cfg/search-mode):2에서는 사용할 수 없습니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|기능 사용 안 함|
|`1(true)`|드래그한 셀들 체크/체크해제 (`default`)|

### Example
```javascript
var opt = {
    Cols:[
        ...,
        // 단일 Bool 타입 컬럼 드래그시 선택할 셀들을 체크합니다.
        {
            Header: { Value: "체크박스(Bool)", HeaderCheck: 1 },
            Type: "Bool",
            Name: "CheckData",
            Width: 80,
            Align: "Center",
            CanEdit: 1,
            SelectCheck: 1,
        }
    ]
}
```

### Read More
- [Type appendix](/docs/appx/type)

### Since

|product|version|desc|
|---|---|---|
|core|8.2.0.26|기능 추가|
