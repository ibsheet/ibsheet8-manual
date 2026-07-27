# CanResize ***(col)***

> 해당 컬럼의 열 너비(column width) 변경 가능 여부를 설정합니다.  
> 사용자가 헤더 영역에서 컬럼 경계선을 드래그하여 열 너비를 조정할 수 있는지 여부를 제어합니다.  
> `Cfg.CanColResize`가 `false`이면 `CanResize` 설정과 관계없이 열 너비 조정은 불가능합니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|사용자 열 너비 변경 불가|
|`1(true)`|사용자 열 너비 변경 가능 (`default`)|


### Example
```javascript
//특정 컬럼만 너비 조정 불가
options.Cols = [

    {Type: "Date", Name: "kDate", Width: 110, CanResize: 0},
];
```

### Read More
- [CanColResize cfg](/docs/props/cfg/can-col-resize)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
