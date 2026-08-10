# setSheetSize ***(method)***

<!-- synonyms: set sheet size, sheet size adjust, sheet width height, set sheet width height, sheet resize, div container size, 시트 크기 조정, 시트 사이즈 변경, 시트 너비 높이, 시트 리사이즈, div 크기 조정, setSheetSize 메소드 -->

> 시트의 태그 사이즈를 조정합니다. 해당 기능은 시트를 감싸고 있는 div 크기를 변화시킵니다. 
>
> number 입력시 px 로 자동으로 치환합니다. 
>
> 단위를 붙여서 입력시 그대로 입력됩니다. 

### Syntax
```javascript
void setSheetSize( width, height );
```

### Parameters

|Name|Type|Required|Description|
|----------|-----|---|----|
|width|`number`|<span class='optional'>선택</span>|설정할 시트 태그 너비|
|height|`number`|<span class='optional'>선택</span>|설정할 시트 태그 높이|

### Return Value
***none***

### Example
```javascript
// 시트의 태그 사이즈를 너비 500 px, 높이 800px로 설정합니다.
sheet.setSheetSize(500, 800);
```

### Read More

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
