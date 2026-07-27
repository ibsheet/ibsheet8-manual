# SelFocusColor ***(cfg)***

> 시트 포커스 혹은 영역 선택시 헤더행과 SEQ 컬럼행의 배경색이 변경됩니다.
>
> 적용 되는 색상은 `.header-Focus`, `.seq-Focus` css 클래스를 통해 적용하실 수 있습니다.

### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`0`|기능 사용 안함 (`default`)|
|`1`|헤더행과 SEQ 컬럼행의 배경색 변경 적용|

### Example
```javascript
options.Cfg = {
    SelFocusColor : 1            // 헤더행과 SEQ 컬럼행의 배경색이 변경
};
```

### Read More

### Since

|product|version|desc|
|---|---|---|
|core|8.1.0.92|기능 추가|