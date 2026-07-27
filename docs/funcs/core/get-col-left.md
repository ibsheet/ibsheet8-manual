# getColLeft ***(method)***

> 특정 열의 위치를 각 섹션의 시작을 기준으로 확인합니다.

### Syntax
```javascript
number getColLeft( col );
```

### Parameters
|Name|Type|Required|Description|
|----------|-----|---|----|
|col|`string`|<span class='required'>필수</span>|확인하고자 하는 열이름|


### Return Value
***number*** : 섹션의 최좌측부터 현재 열의 왼쪽 끝부분까지의 거리(px 단위)

### Example
```javascript
//AMT 열의 x축 offset 값을 확인
var colOff = sheet.getColLeft("AMT");
```

### Read More


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
