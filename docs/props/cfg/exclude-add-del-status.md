# ExcludeAddDelStatus ***(cfg)***

<!-- synonyms: ExcludeAddDelStatus, exclude added deleted, added deleted exclude, save json exclude, doSave filter, 추가 삭제 제외, Added Deleted 제외, 저장 시 제외, getSaveJson 제외, doSave 상태 제외, 추가 후 삭제 행 제외 -->

> 행 추출 함수 사용시 상태가 `Added` 이면서 `Deleted` 인 행의 추출 제외 여부를 설정합니다. 
>
> 기본 동작은 `0(사용 안함, 추출됨)` 이고 `1(사용, 추출 제외)` 로 설정시 해당 상태인 행이 추출되지 않습니다. 
>
> 저장 관련 데이터 추출 함수 (`getSaveJson`, `getSaveString`, `doSave`) 호출에 적용 됩니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
| `0 (false)` | 행 상태가 `Added:1, Deleted:1` 인 행 추출 됨 (`default`) |
| `1 (true)` | 행 상태가 `Added:1, Deleted:1` 인 행은 추출 제외됨|


### Examples
```js
options = {
  Cfg:{
    ExcludeAddDelStatus: 1   // Added:1, Deleted:1 인 행 추출 제외 
  }
};
```

### Read More
- [Deleted row](../../props/row/deleted)
- [Added row](../../props/row/added)
- [getSaveJson](../../funcs/core/get-save-json)
- [getSaveString](../../funcs/core/get-save-string)
- [doSave](../../funcs/core/do-save)


### Since

|product|version|desc|
|---|---|---|
|core|8.3.0.38|기능 추가|
