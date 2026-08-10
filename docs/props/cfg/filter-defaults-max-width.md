# FilterDefaultsMaxWidth ***(cfg)***

<!-- synonyms: FilterDefaultsMaxWidth, filter defaults max width, filter menu max width, defaults filter width, filter width limit, 필터 최대 너비, 필터 메뉴 너비, Defaults 필터 너비, 필터 너비 제한, 필터 max width, 필터 가로 스크롤 -->

> 필터 행에서 [Defaults](/docs/props/col/defaults) 를 사용할 때 생성되는 필터 메뉴의 `MaxWidth` 를 설정합니다. 
>
> 생성될 필터 메뉴의 width 가 설정하는 값보다 작은 경우에는 기존의 생성될 width 가 우선되고, 설정하는 값보다 큰 경우에 필터 메뉴의 너비 축소 및 가로 스크롤이 생성됩니다. 

### Type
`number`


### Options

|Value|Description|
|-----|-----|
|`number`|필터의 Defaults 메뉴의 Maxwidth|


### Example
```javascript
options.Cfg = {
    FilterDefaultsMaxWidth: 500
};
```

### Read More
 - [Defaults col](/docs/props/col/defaults)
 - [FilterEnumIconLeft cfg](./filter-enum-icon-left)

### Since

|product|version|desc|
|---|---|---|
|core|8.3.0.34|기능 추가|
