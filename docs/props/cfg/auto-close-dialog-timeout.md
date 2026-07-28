# AutoCloseDialogTimeout ***(cfg)***

> `(Cfg) AutoCloseDialog`가 `true`일 때,
> 마우스 커서가 다이얼로그 영역을 벗어난 이후
> 다이얼로그가 자동으로 닫히기까지의 지연 시간을 설정합니다.

<!-- synonyms: auto close delay, dialog close delay, popup close timeout, close delay ms, 자동 닫기 지연 시간, 메뉴 닫힘 지연 -->


### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`number`|다이얼로그가 자동으로 닫히기까지의 지연 시간(밀리초 단위)|


### Example
```javascript
options = {
  Cfg:{
    AutoCloseDialog: true,
    AutoCloseDialogTimeout: 1000,  // 1초 후 다이얼로그가 자동으로 닫히도록 설정
  }
};
```

### Read More
- [AutoCloseDialog cfg](./auto-close-dialog)

### Since

|product|version|desc|
|---|---|---|
|core|8.3.0.24|기능 추가|
