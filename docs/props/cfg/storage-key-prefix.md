# StorageKeyPrefix ***(cfg)***

<!-- synonyms: StorageKeyPrefix, storage key prefix, local storage prefix, session storage prefix, document url key, 스토리지 프리픽스, 로컬 스토리지 prefix, 세션 스토리지 prefix, 저장 키 접두사, URL 키 유실 방지 -->

> 로컬 스토리지 혹은 세션 스토리지에 현재 시트의 정보가 저장될 때 사용되는 Key값의 `prefix`를 설정하는 옵션입니다.  
> 실제 저장 Key는 `StorageKeyPrefix + "^" + 시트id` 형식으로 구성됩니다.  
> 값을 설정하지 않으면 `document.URL`이 기본값으로 사용됩니다.  
> [StorageSession](./storage-session) 값이 없으면 동작하지 않습니다.

### 주의 — URL 변경 시 저장값 유실

`StorageKeyPrefix`를 설정하지 않으면 `document.URL`이 Key로 사용됩니다.
URL이 변경되면 이전에 저장한 정보를 찾을 수 없게 되므로, **페이지마다 고정된 고유 문자열을 직접 지정하는 것을 권장합니다.**


### Type
`string`


### Example
```javascript
// URL에서 파일명을 자동 추출하여 prefix로 사용합니다.
// /product/productList.jsp → "productList", /product/productDetail.jsp → "productDetail"
var pageName = location.pathname.split('/').pop().split('.')[0];

options.Cfg = {
    StorageSession: 1,
    StorageKeyPrefix: pageName   // 실제 저장 Key: "productList^sheet"
};

sheet.saveCurrentInfo();      // 로컬 스토리지에 현재 시트 정보를 저장
```

### Read More
- [StorageSession cfg](./storage-session)
- [StorageCompressMode cfg](./storage-compress-mode)
- [saveCurrentInfo method](/docs/funcs/core/save-current-info)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
