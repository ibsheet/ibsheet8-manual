# getSheetFocused ***(method)***

> 현재 포커스된 시트 객체를 반환합니다.  
> 호출한 시트 인스턴스와 상관없이, 현재 화면에서 포커스를 가진 시트를 반환합니다. 

### Syntax
```javascript
void getSheetFocused();
```

### Return Value
***Sheet*** 시트 객체 (포커스된 시트가 없으면 `null`)


### Example
```javascript
// 한 화면에 여러 시트가 있을 때 현재 포커스(선택)된 시트를 확인
var focused = sheet.getSheetFocused();
if (focused) {
    console.log("포커스된 시트 id:", focused.id);
}
```

### Read More

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
