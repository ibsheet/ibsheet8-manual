# StorageCompressMode ***(cfg)***

<!-- synonyms: StorageCompressMode, storage compress mode, local storage compress, session storage compress, base64 utf16 compression, 스토리지 압축, 로컬 스토리지 압축, 세션 스토리지 압축, base64 압축, UTF16 압축, 저장 크기 최적화 -->

> 로컬 스토리지 혹은 세션 스토리지에 저장되는 시트 정보의 압축 방식을 설정하는 옵션입니다.  
> 저장 데이터의 크기를 줄여 브라우저 스토리지 용량 제한에 대응할 수 있습니다.  
> 대부분의 경우 기본값(`1`, Base64)으로 충분합니다.  
> [StorageSession](./storage-session) 값이 없으면 동작하지 않습니다.


### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`0`|UTF16 압축 — 압축률 가장 높음. 저장 용량을 최소화할 때 사용|
|`1`|Base64 압축 — 압축률 중간. 대부분의 환경에서 권장 (`default`)|
|`2`|Uint8Array 압축 — 압축률 가장 낮음|


### Example
```javascript
options.Cfg = {
    StorageSession: 1,       // 로컬 스토리지에 현재 시트 정보를 저장할 수 있고 가져올 수 있도록 설정
    StorageCompressMode: 0   // UTF16 압축으로 로컬 스토리지에 저장
};

sheet.saveCurrentInfo();      // 로컬 스토리지에 현재 시트 정보를 저장
```

### Read More
- [StorageSession cfg](./storage-session)
- [StorageKeyPrefix cfg](./storage-key-prefix)
- [saveCurrentInfo method](/docs/funcs/core/save-current-info)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
