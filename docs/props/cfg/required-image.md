# RequiredImage ***(cfg)***

<!-- synonyms: RequiredImage, required image, required icon, required mark image, custom required image, 필수 입력 이미지, 필수 항목 이미지, Required 아이콘, 필수 표시 이미지, Required 마크 이미지 -->

> 필수 입력 항목 이미지를 기본 이미지와 다르게 바꾸고 싶은 경우, 필수 입력 항목에 대한 표시 이미지 경로를 설정 합니다. 

### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`string`|필수 입력 항목 이미지 경로|


### Example
```javascript
options = {
    Cfg:{
      RequiredImage: "./required.png", // 필수 입력 항목 이미지 경로를 설정
    },
};
```

### Read More
- [Required col](/docs/props/col/required)

### Since

|product|version|desc|
|---|---|---|
|core|8.2.0.23|기능 추가|
