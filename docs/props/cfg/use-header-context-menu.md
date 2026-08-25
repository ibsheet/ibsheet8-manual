# UseHeaderContextMenu ***(cfg)***

<!-- synonyms: UseHeaderContextMenu, use header context menu, header right click menu, header context menu, header contextmenu, 헤더 컨텍스트 메뉴, 헤더 우클릭 메뉴, 헤더 오른쪽 클릭 메뉴, 헤더 메뉴 표시 -->

> 헤더 컨텍스트 메뉴의 표시 여부를 제어합니다.  
> 기본 메뉴는 `ibsheet-common.js`에 정의되어 있으며, 이 파일이 포함된 경우 기본값(`1`)에서 표시됩니다.


### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|헤더 컨텍스트 메뉴 표시 안 함|
|`1(true)`|헤더 컨텍스트 메뉴 표시 (`default`)|

### Example
```javascript
options.Cfg = {
    UseHeaderContextMenu: false              // 헤더 컨텍스트 메뉴 표시 안 함
};
```

![헤더 컨텍스트 메뉴](/assets/imgs/header_context_menu.png "헤더 우클릭 시 나타나는 기본 컨텍스트 메뉴")

### Read More
- [menu appendix](/docs/appx/menu)

### Since

|product|version|desc|
|---|---|---|
|core|8.2.0.1|기능 추가|