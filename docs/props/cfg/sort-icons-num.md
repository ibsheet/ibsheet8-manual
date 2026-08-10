# SortIconsNum ***(cfg)***

<!-- synonyms: SortIconsNum, sort icons num, sort priority number, multi sort number, sort order number, 정렬 순서 숫자, 소팅 순위 숫자, 다중 정렬 번호, 정렬 우선순위 표시, 소팅 아이콘 숫자 -->

> 다중 컬럼 소팅시 소팅 적용 순위를 소팅 아이콘 우측에 숫자로 표시합니다. 

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|다중 컬럼 소팅시 소팅 적용 순위를 숫자로 표시하지 않습니다. (`default`)|
|`1(true)`|다중 컬럼 소팅시 소팅 적용 순위를 숫자로 표시합니다.|

### Example
```javascript
//다중 컬럼 소팅시 소팅 우선순위를 숫자로 표시합니다.
options.Cfg = {
    SortIconsNum: true
};
```

### Read More

### Since

|product|version|desc|
|---|---|---|
|core|8.1.0.102|기능 추가|
<!--!|`[비공개]` core-lwc|8.1.1.98|기능 추가|
!-->