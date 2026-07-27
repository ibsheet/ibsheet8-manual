# revertCol ***(method)***

<!-- synonyms: 컬럼 되돌리기, 컬럼 복원, 레이아웃 초기화, revert col -->

> 시트 생성 시점의 컬럼 정보(너비, 순서, 숨김 여부, 정렬)로 되돌리는 메소드입니다.
>
> 시트 생성이 완료되는 시점([onRenderFirstFinish](/docs/props/event/on-render-first-finish))에 자동으로 컬럼 상태를 스냅샷으로 저장하며, `revertCol` 호출 시 이 스냅샷을 기준으로 복원합니다.
>
> 사용자가 컬럼을 숨기거나, 너비를 조절하거나, 순서를 변경하거나, 동적으로 삭제/추가한 컬럼 상태 모두 create 시점으로 돌아갑니다.
> 컬럼너비, 순서, 숨김 여부, 정렬 이외의 변경과 행/셀 데이터에는 영향을 주지 않습니다.

### Syntax
```javascript
boolean revertCol();
```

### Return Value
***boolean*** : 되돌리기 완료 여부

### Example
```javascript
// 컬럼 숨김/너비 조절/순서 변경 후 원래대로 되돌림
sheet.hideCol("TextData");
sheet.setAttirubte(null, "IntData", "Width", 200);

// 변경된 모든 컬럼 상태가 시트 생성 시점으로 복원됨
sheet.revertCol();
```

```javascript
// addCol/deleteCol 후 복원 시
sheet.addCol("NewCol", 0, null, { Type: "Text", Header: "추가" });
sheet.deleteCol("OldCol");

// 추가했던 NewCol은 제거되고, 삭제했던 OldCol은 다시 생성됨
sheet.revertCol();
```


### Since

|product|version|desc|
|---|---|---|
|core|8.4.0.1|기능 추가|
