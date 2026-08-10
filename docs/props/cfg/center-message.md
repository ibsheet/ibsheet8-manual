# CenterMessage ***(cfg)***

<!-- synonyms: CenterMessage, center message, screen center message, sheet message position, message center, 메시지 중앙 표시, 화면 중앙 메시지, 시트 메시지 위치, 브라우저 중앙 메시지, 메시지 정렬, 메시지 위치, 화면 중앙 안내 -->

> 시트에서 표시되는 메시지를 시트 위치와 무관하게 화면 중앙에 표시할지 여부를 설정합니다.  
> 해당 속성을 설정하지 않으면, 메시지는 시트 영역의 중앙에 표시됩니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|시트 영역 중앙에 메시지 표시 (`default`)|
|`1(true)`|브라우저 화면 중앙에 메시지 표시|


### Example
```javascript
options = {
    "Cfg":{
      "CenterMessage": true,  // 메시지를 화면 중앙에 표시
    }
};
```

### Read More
- [showMessage cfg](./suppress-message) 
- [showMessageTime method](/docs/funcs/core/show-message-time) 
- [SuppressMessage cfg](./suppress-message) 

### Since
|product|version|desc|
|---|---|---|
|core|8.0.0.1|기능 추가|
