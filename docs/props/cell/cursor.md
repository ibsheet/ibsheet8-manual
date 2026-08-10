# Cursor ***(cell)***

<!-- synonyms: 커서 모양, 마우스 커서, 셀 커서, 호버 커서, pointer 커서, css 커서, 커서 스타일, cursor, mouse cursor, cell cursor, hover cursor, css cursor, pointer, crosshair -->

> 셀 위에 마우스 커서가 호버시 커서의 모양을 설정합니다.
>
> 설정가능한 커서의 모양은 css를 따릅니다.
>
> ex) auto, crosshair, default, pointer, move, e-resize, ne-resize, nw-resize, n-resize, se-resize, sw-resize, w-resize, text, wait, help


### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`string`|원하는 커서 모양|


### Example
```javascript
//셀에 커서가 들어갔을때 커서 모양을 클릭가능한 손가락 모양으로 변경.
{
    data:[
        {... , "CLSCursor":"pointer" , ...}
    ]
}
```

### Read More
- [Cursor col](/docs/props/col/cursor)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
