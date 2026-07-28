# clearCurrentInfo ***(method)***

<!-- synonyms: 저장된 컬럼 정보 삭제, 스토리지 정보 삭제, 레이아웃 삭제, 로컬 스토리지 삭제, 세션 스토리지 삭제, clear current info, remove saved column layout -->

> [saveCurrentInfo](./save-current-info)로 저장된 현재 시트의 컬럼 정보를 로컬 스토리지 혹은 세션 스토리지에서 제거하는 메소드입니다.  
> [StorageSession](/docs/props/cfg/storage-session) 값이 0인 경우에는 제거 동작을 하지 않습니다.

### Syntax
```javascript
boolean clearCurrentInfo();
```

### Return Value
***boolean*** : 성공 시 `true`, 실패 시 `false` (로컬 스토리지 혹은 세션 스토리지에서 시트 정보 제거에 실패했을 때)

### Example
```javascript
options.Cfg = {
    StorageSession: 1  // 로컬 스토리지에 현재 시트 정보를 저장할 수 있도록 설정
};
```

```javascript
// 저장된 시트 정보를 제거한다.
if (sheet.clearCurrentInfo()) {
    alert("저장된 시트 정보를 제거했습니다.");
}
```

### Read More
- [saveCurrentInfo method](./save-current-info)
- [getSavedCurrentInfo method](./get-saved-current-info)
- [StorageSession cfg](/docs/props/cfg/storage-session)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
