# Checked ***(cell)***

<!-- synonyms: 아이콘 체크 상태, 셀 체크 여부, Icon Check, Button Check, {컬럼명}Checked -->

> [Icon](/docs/props/col/icon)이나 [Button](/docs/props/col/button) 속성을 `"Check"`로 설정해 셀 좌/우측에 표시된 별도 체크박스의 체크 상태를 다룹니다.  
> 데이터 키는 `{컬럼명}Checked` 형식이며, 조회 데이터에 포함하거나 [setIconCheck](/docs/funcs/core/set-icon-check)로 설정할 수 있습니다.  
> 단, 저장 함수([getSaveJson](/docs/funcs/core/get-save-json) 등) 호출 시에는 기본적으로 `{컬럼명}Checked` 값이 추출되지 않습니다.  
> 추출하려면 `saveAttr` 옵션에 키를 명시합니다.

###
![ICON Check](/assets/imgs/iconCheck.png "Icon:Check 사용한 경우")

### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`0` | 체크해제됨|
|`1` | 체크됨|
|`2` | 알 수 없음 (체크박스 안에 `?` 표시)|

### Example
```javascript
// 1. 컬럼 설정 — Icon이나 Button을 "Check"로 지정해야 체크박스가 표시됨
options.Cols = [
    {Header: "분류", Type: "Text", Name: "Cls", Icon: "Check"}
];

// 2. setIconCheck로 특정 셀 체크
sheet.setIconCheck(sheet.getRowById("AR9"), "Cls", 1);

// 3. 행 객체에서 직접 체크 상태 읽기 ({컬럼명}Checked)
var row = sheet.getRowById("AR10");
var isChecked = row["ClsChecked"];

// 4. 조회 데이터에 체크 상태 포함
{
    "data": [
        { ..., "ClsChecked": 1, ... }
    ]
}

// 5. 저장 시 체크 값 함께 추출 — saveAttr 옵션 사용
var saveData = sheet.getSaveJson({saveAttr: "ClsChecked"});
```

### Read More
- [Icon col](/docs/props/col/icon)
- [Button col](/docs/props/col/button)
- [setIconCheck method](/docs/funcs/core/set-icon-check)
- [onIconClick event](/docs/events/on-icon-click)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
