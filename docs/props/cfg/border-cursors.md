# BorderCursors ***(cfg)***

>  (cfg)[Hover](./hover) : 2가 설정된 시트에서, 호버된 행의 `Border` 표시 여부를 설정합니다.

### 옵션별 동작 이미지
![borderCursors](/assets/imgs/borderCursors1.png "borderCursors")<br/>
> 호버된 행에 Border 표시

![borderCursors](/assets/imgs/borderCursors0.png "borderCursors")<br/>
>호버된 행과 셀의 Border 표시 안함

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|호버된 행 `Border` 표시 안함|
|`1(true)`|호버된 행 `Border` 표시(`default`)  |


### Example
```javascript
options = {
  Cfg : {
    "Hover": 2,                  // 행단위 Hover 동작
    "BorderCursors": true,       // Hover 행과 셀의 Border 표시
  }
};
```

### Read More
- [Hover cfg](./hover)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
