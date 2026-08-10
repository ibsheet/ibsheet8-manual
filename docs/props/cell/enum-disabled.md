# EnumDisabled ***(cell)***

<!-- synonyms: 콤보 항목 비활성화, Enum 아이템 비활성, 드롭다운 비활성, 아이템 선택 불가, 드랍리스트 비활성, 콤보 항목 잠금, enum-disabled, enum disabled, dropdown item disable, disable enum item, combo item disabled -->

> [Enum](./enum) 속성을 통해 설정한 아이템들의 선택 불가능 여부를 설정합니다.
>
> 첫번째 글자를 구분자로 설정하게 됩니다. 

### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`string`|첫번째 글자를 구분자로 하는 문자열 (ex:"#1#0")|

### Example
```javascript
//1. 메소드를 통해 특정 셀에 속성 적용 (열이름 :CLS )
sheet.setAttribute(sheet.getRowById("AR99"), "CLS", "EnumDisabled", "|1|0|0|0|0|1|0|1|1|0|0");


//2. 객체에 직접 접근해서 속성 적용 (열이름 :CLS )
var ROW = sheet.getRowById("AR10");
ROW["CLSEnumDisabled"] = "|1|0|0|0";
//변경내용 확인
sheet.refreshCell({row:ROW, col:"CLS"});


//3. 조회 데이터 내에서 속성 적용  (열이름 :CLS )
{
    data:[
        {..., "CLSEnumDisabled":"|1|0", ...}
    ]
}
```

### Read More
- [Enum cell](./enum)
- [EnumKeys cell](./enum-keys)
- [EnumMenu cell](./enum-menu)

### Since

|product|version|desc|
|---|---|---|
|core|8.3.0.16|기능 추가|
