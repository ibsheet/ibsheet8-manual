# getSavedCurrentInfo ***(method)***

<!-- synonyms: 저장된 컬럼 정보 조회, 스토리지 컬럼 정보 조회, 로컬 스토리지 조회, 세션 스토리지 조회, 저장 레이아웃 조회, get saved current info, read saved column layout -->

> [saveCurrentInfo](./save-current-info)로 로컬 스토리지 혹은 세션 스토리지에 저장된 시트의 컬럼 정보를 문자열로 가져옵니다.

### Syntax
```javascript
string getSavedCurrentInfo();
```

### Return Value
***string*** : 저장된 컬럼들의 숨김, 너비, 위치 정보를 담은 문자열. 저장된 정보가 없을 경우 문자열 `"false"` 반환.

### Example
```javascript
// 반환값이 "false"(문자열)일 수 있으므로 반드시 확인 후 setCurrentInfo에 전달
var savedInfo = sheet.getSavedCurrentInfo();
if (savedInfo !== "false") {
    sheet.setCurrentInfo(savedInfo);
} else {
    console.log("저장된 레이아웃이 없습니다.");
}
```

### Read More
- [saveCurrentInfo method](./save-current-info)
- [clearCurrentInfo method](./clear-current-info)

### Since

|product|version|desc|
|---|---|---|
|core|8.3.0.28|기능 추가|
