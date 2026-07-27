# saveCurrentInfo ***(method)***
> 현재 시트의 컬럼 정보(순서, 너비, 숨김 등)를 **로컬/세션 스토리지에 자동 저장**합니다. 별도 저장 코드 없이 브라우저 개인화에 활용할 수 있습니다.
>
> 기본적으로 Key값은 [StorageKeyPrefix](/docs/props/cfg/storage-key-prefix)+"^시트id" 로 설정됩니다.
>
> 저장되는 값은 [StorageCompressMode](/docs/props/cfg/storage-compress-mode)에 따라 압축되어서 저장됩니다.
>
> [StorageSession](/docs/props/cfg/storage-session) 값이 없으면 동작하지 않습니다.

### Syntax
```javascript
boolean saveCurrentInfo();
```

### Return Value
***boolean*** : 성공 시 `true`, 실패 시 `false`

### Example
```javascript
options.Cfg = {
    StorageSession: 1  // 로컬 스토리지에 현재 시트 정보를 저장할 수 있도록 설정
};
```

```javascript
// 현재 시트의 정보를 로컬 스토리지 혹은 세션 스토리지에 저장한다.
if (sheet.saveCurrentInfo()) {
    alert("현재 시트 정보를 저장했습니다.");
} else {
    alert("현재 시트 정보를 저장하는데 실패했습니다.");
}

// 저장된 정보는 window.localStorage에서 확인할 수 있다.
// Key 형식: StorageKeyPrefix + "^" + 시트id
console.log(window.localStorage);
```

### Read More
- [getSavedCurrentInfo method](./get-saved-current-info)
- [clearCurrentInfo method](./clear-current-info)
- [StorageSession cfg](/docs/props/cfg/storage-session)
- [StorageKeyPrefix cfg](/docs/props/cfg/storage-key-prefix)
- [StorageCompressMode cfg](/docs/props/cfg/storage-compress-mode)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
