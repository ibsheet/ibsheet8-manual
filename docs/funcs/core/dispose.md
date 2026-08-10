# dispose ***(method)***

<!-- synonyms: 시트 제거, 시트 삭제, 메모리 해제, 완전 제거, 시트 파괴, DOM 제거, dispose, destroy, remove sheet, cleanup, unmount, teardown -->

> 시트를 DOM과 메모리에서 완전히 제거합니다.  
> `dispose`된 시트는 더 이상 사용할 수 없으며, 다시 사용하려면 [IBSheet.create](/docs/static/create)로 처음부터 새로 생성해야 합니다.  
> `dispose`는 **호출한 시트 하나**만 제거합니다. 한 화면(페이지)의 시트를 모두 제거하려면(특히 SPA 페이지 이동 시) [IBSheet.disposeAll](/docs/static/dispose-all)을 사용합니다.  
> SPA(Single Page Application) 기반 프로젝트에서는 페이지가 바뀌기 전에 시트 객체를 제거해야 합니다.  
> `dispose` 후에는 해당 시트가 담겨 있던 `IBSheet` 배열의 원소가 `null`이 됩니다.  
> **<mark>주의</mark> : 이 `null` 원소를 배열에서 제거(`splice` 등)하지 마세요.   
> 배열의 순서(인덱스)가 바뀌어 시트 인덱스 참조가 깨집니다.** `IBSheet` 배열을 순회할 때는 `null` 원소를 건너뛰기만 하세요.

### Syntax
```javascript
void dispose();
```


### Return Value
***none***

### Example
```javascript
// 시트 객체를 완전히 제거
sheet.dispose();

// 같은 id/div에 다시 생성하기 전, 기존 시트가 있으면 제거 (중복 id 방지)
if (IBSheet.hasSheet("sheet")) {
    sheet.dispose();
}

IBSheet.create({ id: "sheet", el: "sheetDiv", options: OPT });
```

### Read More

- [IBSheet.hasSheet static](/docs/static/has-sheet)
- [IBSheet.disposeAll static](/docs/static/dispose-all)
- [IBSheet.create static](/docs/static/create)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
