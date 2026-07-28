# AutoCloseDialog ***(cfg)***
> IBSheet 내부에서 사용하는 다이얼로그(예: `달력`, `컨텍스트 메뉴`, `UseFilterDialog:1` 사용시 등)가  
> 마우스 커서가 해당 다이얼로그 영역을 벗어날 때 자동으로 닫힐지 여부를 설정합니다.


<!-- synonyms: auto close dialog, auto close popup, close on mouse leave, popup auto close, dialog auto hide, 자동 닫기, 메뉴 자동 닫기, 마우스 벗어나면 닫기 -->


### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`false`|자동 닫기 사용 안함. (`default`)|
|`true`|마우스가 다이얼로그 영역을 벗어나면 자동으로 닫힘|


### Example
```javascript
options = {
  "Cfg":{
    "AutoCloseDialog": true,  // 마우스가 벗어날 때 다이얼로그를 자동으로 닫는다.
  }
};
```

### Read More
- [AutoCloseDialogTimeout](./auto-close-dialog-timeout) 

### Since

|product|version|desc|
|---|---|---|
|core|8.3.0.24|기능 추가|
