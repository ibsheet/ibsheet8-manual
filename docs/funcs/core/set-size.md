# setSize ***(method)***

<!-- synonyms: setSize, set-size, 크기 설정, 사이즈 변경, Size 속성, 시트 크기, 크기 변경, 사이즈 설정, size 적용, size, set size, change size, apply size, resize -->

> [(Cfg) Size](/docs/props/cfg/size) 설정을 동적으로 변경합니다 

### Syntax
```javascript
void setSize( size );
```

### Parameters
|Name|Type|Required| Description |
|----------|-----|---|----|
|size|`string`|<span class='required'>필수</span>|설정할 `Size` 속성|


### Return Value
***none***

### Example
```javascript
// 시트 Cfg.Size 설정 "Tiny"로 변경
sheet.setSize('Tiny');
```

### Try it

- [Demo of setSize](https://jsfiddle.net/gh/get/library/pure/ibsheet/ibsheet8-manual-sample/tree/master/samples/properties/Cfg/Size/)

### Read More
- [Size cfg](/docs/props/cfg/size)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.13|기능 추가|
