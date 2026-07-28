# ClearFilterOff ***(cfg)***
> 필터 행에서 연산자 `사용안함`을 선택했을 때, 해당 필터 셀의 값을 유지할지 또는 삭제할지 여부를 설정합니다.  
> 연산자 `사용안함` 선택 시 필터 조건은 해제되며, 이때 입력된 필터 값의 유지 여부를 제어합니다.
>
> 기본값은 값을 유지합니다.


<!-- synonyms: filter off clear, clear filter value, remove filter value, filter operator X, 필터 값 삭제, 필터 초기화 -->


### Type
`number`

### Options
|Value|Description|예시|
|-----|-----|-----|
|`0`|필터 `사용안함` 선택 시 값 유지 (`default`)|![ClearFilterOff : 0](/assets/imgs/ClearFilterOff-0.gif "ClearFilterOff : 0")|
|`1`|필터 `사용안함` 선택 시 값 삭제|![ClearFilterOff : 1](/assets/imgs/ClearFilterOff-1.gif "ClearFilterOff :1")|


### Example
```javascript
options = {
  "Cfg":{
    "ShowFilter":1,      // 필터행 표시
    "ClearFilterOff":1,  // 필터행에서 사용안함 선택시 필터셀 값 삭제
  }
};
```

### Read More
- [ShowFilter cfg](./show-filter) 

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
