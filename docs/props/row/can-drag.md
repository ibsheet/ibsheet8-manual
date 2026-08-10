# CanDrag ***(row)***

<!-- synonyms: row can drag, draggable row, row drag enabled, row reorder, row order change, drag row, per-row drag, 행 드래그, 행 드래그 허용, 드래그 가능 여부, 순서 변경 제한, 행 이동, CanDrag row -->
> 해당 행의 드래그 가능 여부를 설정합니다.  
> `cfg.CanDrag`가 `true`인 경우에만 적용됩니다.  
> 특정 행의 순서 변경(row reorder)을 제한할 때 사용합니다.


### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|드래그 불가|
|`1(true)`|드래그 가능|



### Example
```javascript
// 특정 행의 드래그를 제한
var row = sheet.getRowById("AR5");
row["CanDrag"] = 0;
```

### Read More
- [CanDrag cfg](/docs/props/cfg/can-drag)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
