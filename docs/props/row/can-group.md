# CanGroup ***(row)***

<!-- synonyms: row can group, groupable row, row group enabled, exclude from group, standalone row, per-row group, 행 그룹, 그룹 허용, 그룹핑 가능, 그룹 제외, 독립 행, 그룹핑 여부, CanGroup row -->
> 특정행에 대한 그룹핑 허용 여부를 설정합니다.
>
> `0(false)`로 설정시 해당 행은 그룹에 포함되지 않고 독립적으로 위치하게 됩니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|그룹핑 불가|
|`1(true)`|그룹핑  가능|


### Example
```javascript
//특정행들은 그룹에서 제외 시킨다.
{"data":[
    ...
    {"CanGroup":0,"ColName1":"Value1","ColName2":"Value2", ...},
    ...
]}
```

### Read More
- [Group cfg](/docs/props/cfg/group)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
