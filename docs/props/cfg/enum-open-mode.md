# EnumOpenMode ***(cfg)***

<!-- synonyms: EnumOpenMode, enum open mode, enum list open, dropdown auto open, combo auto open, enum focus open, Enum 열기, Enum 리스트 표시, 콤보 자동 열기, 드롭다운 자동 열기, 포커스 시 Enum, Enum 목록 자동 -->

> 포커스 이동 간에 Enum목록 열기 방법을 설정합니다. 

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|포커스 시 Enum 리스트 목록을 표시하지 않음|
|`1(true)`|포커스 시 Enum 리스트 목록을 표시 (`default`)|

### Example
```javascript
options.Cfg = {
  EnumOpenMode: false      // 포커스 시 Enum 리스트 목록을 표시하지 않음
};
```

### Read More


### Since

|product|version|desc|
|---|---|---|
|core|8.3.0.11|기능 추가|
