# DataAutoTrim ***(cfg)***
> 데이터의 앞뒤 공백(trim)을 자동으로 제거할지 여부를 설정합니다.  
> `true`로 설정하면 다음 상황에서 값의 앞뒤 공백이 자동으로 제거됩니다.
> - 조회(Search)로 데이터를 로드할 때
> - 사용자가 셀 값을 입력할 때
> - `setValue` API로 값을 설정할 때

### 주의
- 데이터를 로드할 때 모든 문자열에 대해 trim 처리가 수행되므로  
  데이터 양이 많은 경우 조회 성능에 영향을 줄 수 있습니다.

<!-- synonyms: data trim, auto trim, remove whitespace, 문자열 공백 제거, 데이터 공백 제거, trim option -->

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
| `0` (`false`) | 데이터의 앞뒤 공백을 제거하지 않음 (`default`) |
| `1` (`true`)  | 조회, 입력, `setValue` 시 데이터의 앞뒤 공백을 자동 제거 |


### Example
```javascript
// 조회 및 입력 시 모든 데이터의 앞뒤 공백을 제거
options.Cfg = {
    DataAutoTrim: true
};
```

### Read More
- [SearchMode cfg](/docs/props/cfg/search-mode)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.7|기능 추가|
|core|8.0.0.19|데이터 입력, `setValue` 시에도 공백처리 되도록 추가|
