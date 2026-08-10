# ForceEnterEdit ***(cfg)***

<!-- synonyms: ForceEnterEdit, force enter edit, enter to edit, enter key edit, edit before move, enter edit then move, 엔터 편집 강제, Enter 편집 진입, EnterMode 편집, Enter 편집 후 이동, 강제 편집 진입, Enter 포커스 편집, 편집 없이 이동 -->

> [EnterMode](/docs/props/cfg/enter-mode)의 `mode`가 `0`이 아닌(이동) 경우, 포커스 상태에서 `Enter`를 눌렀을 때 편집을 먼저 시작한 뒤 이동할지(`true`) 아니면 편집 없이 바로 이동할지(`false`)를 설정합니다.


### Type
`boolean`


### Options
|Value|Description|
|-----|-----|
|`0(false)`|포커스 상태에서 편집 전환 없이 바로 `mode` 동작 수행|
|`1(true)`|포커스 상태에서는 편집 상태로 바뀐 후 `EnterMode`의 기본 동작 수행 (`default`)|


### Example
```javascript
options.Cfg = {
   // enter 키 이동시 편집 상태일때는 편집을 종료하고 우측 셀로 이동 (포커스 상태일 때는 우측 셀로 바로 이동)
   EnterMode: 3,
   ForceEnterEdit: false
   ...
};
```

### Read More

- [EnterMode cfg](/docs/props/cfg/enter-mode)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
