# AutoSelectFirstEnum ***(cfg)***

<!-- synonyms: AutoSelectFirstEnum, auto select first enum, first enum item, default enum value, enum default, combo default, 첫 번째 Enum 자동 선택, Enum 첫 항목, 콤보 첫 값, 신규 행 Enum 기본값, EnumKeys 자동 선택, 목록 첫 값 자동 선택, 드롭다운 첫 항목 -->

> 신규 행을 추가하거나 [setAttribute](/docs/funcs/core/set-attribute)로 `Enum` / `EnumKeys`를 설정하는 경우, 
> `Enum` 타입 컬럼의 첫 번째 항목이 자동으로 선택되도록 설정하는 옵션입니다.

### 주의사항
- `setAttribute(null, col, ...)`로 컬럼 전체의 `Enum`/`EnumKeys`를 설정할 경우에는  
  반드시 데이터 로드 이전에 적용해야 첫 번째 항목이 자동 선택됩니다.
- 데이터 로드 이후에는 전체 컬럼 변경 시 자동 선택이 적용되지 않으며,  
  특정 셀(row 지정) 변경 시에만 자동 선택이 동작합니다.
- `setAttribute`로 `Enum` 값을 설정할 경우  
  `EnumKeys`를 먼저 설정한 뒤 `Enum`을 설정해야 정상적으로 동작합니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0` (`false`)|기능 사용 안함 (`default`)|
|`1` (`true`)|목록의 첫 번째 항목 자동 선택|

### Example
```javascript

// 1. 신규 행 추가 시 첫 번째 항목 자동 선택
options = {
   Cfg : {
     AutoSelectFirstEnum : 1
   },
   Cols:[
     {
      "Header": "콤보(Enum)",
      "Type": "Enum",
      "Name": "ComboData", 
      "Enum": "|대기|진행중|완료", 
      "EnumKeys": "|01|02|03" 
     }
   ]
};

sheet.addRow();

// 2. 조회 전 상태에서 setAttribute로 Enum 설정 후 행 추가
options = {
   Cfg : {
     AutoSelectFirstEnum : 1
   },
   Cols:[
     {"Header": "콤보(Enum)","Type": "Enum","Name": "ComboData"}
   ],
   Events : {
     onRenderFirstFinish : function(evtParam) {
       //시트 초기화 완료 후 Enum 셋팅
       //컬럼의 enum 정보를 셋팅시 반드시 조회전에 설정해야 합니다.
       var sheet = evtParam.sheet;
       sheet.setAttribute(null, "ComboData", "EnumKeys", "|101|102");
       sheet.setAttribute(null, "ComboData", "Enum", "|진행중|완료");
     }
   }
};

// 3. 조회 후 특정 셀의 Enum 변경
sheet.setAttribute(sheet.getFocusedRow(), "ComboData", "EnumKeys", "|101|102");
sheet.setAttribute(sheet.getFocusedRow(), "ComboData", "Enum", "|진행중|완료");

```

### Read More
- [addRow method](/docs/funcs/core/add-row)
- [Enum col](/docs/props/col/enum)
- [EnumKeys col](/docs/props/col/enum-keys)
- [setAttribute method](/docs/funcs/core/set-attribute)

### Since

|product|version|desc|
|---|---|---|
|core|8.2.0.5|기능 추가|
