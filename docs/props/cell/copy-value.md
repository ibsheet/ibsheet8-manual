# CopyValue ***(cell)***

> `Ctrl + C`로 셀을 복사할 때 **클립보드에 복사될 값을 설정합니다.**  
> `CopyValue`가 설정된 경우 **셀의 실제 데이터 값 대신 `CopyValue` 값이 복사됩니다.**  
> `Html`, `Button` 등 표시 내용과 실제 데이터가 다른 셀에서 복사 값을 지정할 때 유용합니다.


### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`string`|복사 시 클립보드에 저장될 문자열|


### Example
```javascript
// 1. setAttribute 메서드를 통해 특정 셀 복사 시 실제 값 대신 지정한 문자열이 복사되도록 설정
sheet.setAttribute(sheet.getRowById("AR99"), "CLS", "CopyValue", "복사불가필드");

// 2. 조회 데이터에서 속성 설정 (열 이름이 CLS인 경우)
{
  data: [
    { "CLSCopyValue": "복사불가필드" }
  ]
}

//3. 데이터 행 객체(예: AR10)에 직접 접근하여 셀에 속성 설정(열 이름이 CLS인 경우)
var ROW = sheet.getRowById("AR10");
ROW["CLSCopyValue"] = "복사불가필드";

```

### Read More
- [CanCopyPaste col](/docs/props/col/can-copy-paste)
- [CopyCols cfg](./copy-cols)
- [CopyEdit cfg](./copy-edit)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
