# MoveMessage ***(cfg)***

> 시트 메시지 창의 드래그 여부를 설정합니다.  
>
> `1(true)`로 설정시 사용자가 메세지 장을 드래그를 통해 옮길 수 있습니다.


### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|메세지 창의 드래그 불가능 (`default`)|
|`1(true)`|메세지 창의 드래그 가능|


### Example
```javascript
options.Cfg = {
  MoveMessage: 0,    // 메세지 창 드래깅 가능
  ...
};
```

### Read More
- [SuppressMessage cfg](./suppress-message)
- [MessageWidth cfg](./message-width)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
