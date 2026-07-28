# EditCursor ***(cfg)***
> 편집모드로 진입 시 커서 위치를 지정하는 속성입니다.

### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`0`|편집 모드 진입시 값 전체 선택 (`default`)|
|`1`|편집 모드 진입시 값의 우측 끝으로 커서 이동|
|`2`|편집 모드 진입시 값의 좌측 처음으로 커서 이동|

### Example
```javascript
options.Cfg :{
    // 편집 모드 진입시 값의 우측 끝으로 커서가 이동
    EditCursor: 1
};
```

### Read More
- [EnterMode cfg](./enter-mode)
- [InEditMode cfg](./in-edit-mode)

### Since

|product|version|desc|
|---|---|---|
|core|8.3.0.57|기능 추가|
