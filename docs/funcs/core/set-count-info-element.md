# setCountInfoElement ***(method)***

> [InfoRowConfig cfg](/docs/props/cfg/info-row-config) 기능 사용시 표시되는 데이터 행수 정보를 시트 외부의 Dom Element 에 표시합니다.

### Syntax
```javascript
boolean setCountInfoElement ( element );
```

### Parameters
|Name|Type|Required| Description |
|----------|-----|---|----|
|element |`object` \| `string`|<span class='required'>필수</span>| 데이터 행수 정보를 표시할 Dom Element 또는 해당 id|

### Return Value
***boolean*** : `true`: 외부의 Dom Element 표시 성공 `false`: 실패

### Example
```javascript
// id가 'countElem'인 div 에 데이터 행수 정보 출력 설정
sheet.setCountInfoElement ( 'countElem' );
sheet.setCountInfoElement ( docuemnt.getElementById('countElem') );
```

### Read More
- [InfoRowConfig cfg](/docs/props/cfg/info-row-config)
- [getCountInfoElement method](./get-count-info-element)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.7|기능 추가|