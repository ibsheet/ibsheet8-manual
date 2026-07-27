# StorageSession ***(cfg)***

> 사용자가 컬럼을 숨기거나, 이동하거나, 사이즈를 조절한 상태를 로컬/세션 스토리지에 저장할 수 있도록 설정합니다.  
> [saveCurrentInfo](/docs/funcs/core/save-current-info)로 저장된 정보가 있으면 시트 로드 시 자동으로 이전 레이아웃이 복원됩니다.

### 참고

개발자가 소스에서 컬럼 정의(`Cols`)를 변경(추가/삭제/순서 변경 등)하여 배포한 경우, 스토리지에 저장된 정보와 달라지므로 저장된 정보는 자동으로 삭제되고 `IBSheet.create` 시점의 초기 설정으로 시트가 그려집니다.


### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`0`|사용안함 (`default`)|
|`1`|로컬 스토리지에 저장 — 브라우저를 닫아도 유지됨 (일반적으로 권장)|
|`2`|세션 스토리지에 저장 — 탭/창을 닫으면 삭제됨|


### Example
```javascript
// 시트 생성 시 설정
options.Cfg = {
    StorageSession: 1  // 로컬 스토리지 사용
};
```

> `ibsheet-common.js` 파일을 페이지에 링크하면 헤더 영역 우클릭 메뉴에서 **"컬럼 정보 저장"** / **"컬럼 정보 저장 취소"** 기능이 자동으로 제공됩니다.
>
> ![StorageSession](/assets/imgs/StorageSession.png "헤더 우클릭 메뉴")

```javascript
// 버튼 클릭으로 컬럼 정보 저장/초기화
document.getElementById("btnSave").onclick = function() {
    sheet.saveCurrentInfo();
};

document.getElementById("btnReset").onclick = function() {
    sheet.clearCurrentInfo();
    location.reload();  // 저장 정보 삭제 후 초기 설정으로 시트를 다시 그림
};
```

### Read More
- [StorageKeyPrefix Cfg](./storage-key-prefix)
- [StorageCompressMode Cfg](./storage-compress-mode)
- [UseHeaderContextMenu Cfg](./use-header-context-menu)
- [saveCurrentInfo method](/docs/funcs/core/save-current-info)
- [getSavedCurrentInfo method](/docs/funcs/core/get-saved-current-info)
- [clearCurrentInfo method](/docs/funcs/core/clear-current-info)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
