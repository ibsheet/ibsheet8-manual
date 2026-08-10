# TabStop ***(cfg)***

<!-- synonyms: TabStop, tab stop, sheet tab focus, tab key navigation, focus tab include, 탭 정지, 탭 이동 포함, 시트 탭 포커스, 탭 순서 포함, Tab 키 시트 포함, TabIndex 순서 -->

> 페이지 안의 요소들을 탭 키로 이동하는 순서에 시트를 포함할지 여부를 설정합니다. 
>
> 시트를 포함하는 경우 `TabIndex` 로 `Tab` 순서를 설정 할 수 있습니다.
>
>


### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`0`|페이지 내에서 `Tab` 키로 시트 접근 안됨 |
|`1`|페이지 내에서 `Tab` 키로 시트 접근 가능 (`default`)|


### Example
```javascript
options.Cfg = {
  TabStop: 0,          // 탭키로 시트 접근 허용 안함
  ...
};
```

### Read More
- [TabIndex cfg](./tab-index)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
