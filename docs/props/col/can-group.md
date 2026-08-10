# CanGroup ***(col)***

<!-- synonyms: 그룹핑 가능, 그룹 가능, 그룹핑 제한, 헤더 드래그 그룹, 그룹 컬럼, group enable, grouping, group by, header drag group, groupable -->

> 열의 그룹핑 가능여부를 설정합니다.
>
> 사용자가 헤더 셀을 드래그 하여 동적으로 구성하는 그룹핑 기능에 대해서 특정 열은 그룹핑이 불가능하게끔 설정하실 수 있습니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|그룹핑 불가|
|`1(true)`|그룹핑 가능 (`default`)|


### Example
```javascript
//특정 열에 대해 그룹핑 불허
options.Cols = [
    ...
    {Type: "Text", Name: "SA_DEPTID", CanGroup: 0, ...},
    ...
];
```

### Read More

- [GroupFormat cfg](/docs/props/cfg/group-format)
- [GroupDef col](./group-def)
- [GroupWidth col](./group-width)
- [GroupEmpty col](./group-empty)
- [GroupSole col](./group-sole)
- [GroupSingle col](./group-single)
- [GroupDeleted col](./group-deleted)
- [GroupChar col](./group-char)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
