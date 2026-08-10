# getGroupRows ***(method)***

<!-- synonyms: getGroupRows, get-group-rows, 그룹 행, 그룹 로우, 그룹행 조회, 그룹 목록, 그룹핑 행, 그룹 결과, group, rows -->

> 그룹으로 생성된 그룹행들을 반환합니다.
>
> 리턴 값은 다음과 같습니다
> {그룹 컬럼명1: [컬럼명1로 생성된 그룹 행들], 그룹 컬럼명2 : [컬럼명2로 생성된 그룹 행들], ...}

### Syntax
```javascript
object getGroupRows();
```

### Return Value
***object***

### Example
```javascript
//그룹 행을 얻습니다.
var groupRows = sheet.getGroupRows();
```

### Read More
- [GroupMain cfg](/docs/props/cfg/group-main)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
