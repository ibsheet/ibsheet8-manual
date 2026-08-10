# RequiredPosition ***(cfg)***

<!-- synonyms: RequiredPosition, required position, required mark position, required left right, required none, 필수 표시 위치, Required 위치, 필수 마크 위치, 필수 아이콘 좌우, 필수 표시 없음, Required Left Right None -->

> [Required](/docs/props/col/required)가 보여질 위치를 설정합니다.

### Type
String

### Options
|Value|Description|
|-----|-----|
|`Left`|헤더의 왼쪽에 `Required` 표시를 합니다. (`default`)<br/>![option1](/assets/imgs/required1.png "option1")|
|`Right`|헤더의 오른쪽에 `Required` 표시를 합니다<br/>![option2](/assets/imgs/required2.png "option2")|
|`None`|헤더에 `Required` 마크를 표시하지 않습니다<br/>|


### Example
```javascript
options = {
    Cfg:{
      RequiredPosition: "Right", // 헤더의 오른쪽에 Required를 설정
    },
    Cols : [
      {Type: "Text", Name: "sName", Required: 1 ...},
      {Type: "Int", Name: "ssalary",Width: 70 ...},
    ...
    ];
};
```

### Read More
- [Required col](/docs/props/col/required)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.2.0.13|`None` 옵션 추가|
