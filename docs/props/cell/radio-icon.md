# RadioIcon ***(cell)***

<!-- synonyms: 라디오 아이콘, 라디오 이미지, custom radio, radio icon cell, 라디오 버튼 모양 -->

> `Type:"Radio"`인 셀에서 라디오 아이콘 모양을 변경합니다.  
> 옵션 값으로 내장 아이콘 종류를 숫자(0~6)로 선택하거나, 직접 이미지 경로 문자열을 지정할 수 있습니다.

### 이미지 경로 형식
첫 글자를 구분자로 하여 체크해제/체크 이미지를 이어 붙입니다.

|패턴|용도|예시|
|---|---|---|
|`구분자 + Off + On`|기본 (편집 가능)|`"|Off.gif|On.gif"`|
|`구분자 + Off + On + OffRO + OnRO`|편집 불가 상태 이미지 포함|`"|Off.gif|On.gif|OffRO.gif|OnRO.gif"`|
|`Off1 + On1 + Off2 + On2 + ...`|한 셀에 라디오 아이콘 여러 개를 표시|`"|Off1.gif|On1.gif|Off2.gif|On2.gif"`|

### Type
`mixed`( `string` \| `number` )

### Options (숫자 옵션 — 내장 아이콘)
|Value|Description|
|-----|-----|
|`0` | 기본 내장 라디오 아이콘 / [Range](/docs/props/col/range) 사용 시 내장 체크박스 아이콘 (`default`)|
|`1` | 내장 라디오 아이콘|
|`2` | 내장 체크박스 아이콘|
|`3` | `<input type="radio">` 객체 사용 / [Range](/docs/props/col/range) 사용 시 `<input type="checkbox">` 객체|
|`4` | `<input type="radio">` 객체 사용|
|`5` | `<input type="checkbox">` 객체 사용|
|`6` | 아이콘 표시 안 함|

> `input` 객체를 사용하는 경우 그렇지 않은 옵션보다 성능이 느릴 수 있습니다.

### Example
```javascript
// 1. setAttribute로 특정 셀에 적용 (열이름 CLS)
sheet.setAttribute(sheet.getRowById("AR99"), "CLS", "RadioIcon", "2");

// 2. 행 객체에서 직접 설정 ({컬럼명}RadioIcon)
var row = sheet.getRowById("AR10");
row["CLSRadioIcon"] = "2";
sheet.refreshCell({row: row, col: "CLS"});

// 3. 조회 데이터에 속성 포함
{
    "data": [
        { ..., "CLSRadioIcon": "2", ... }
    ]
}
```

### Read More
- [RadioIcon col](/docs/props/col/radio-icon)
- [RadioIconWidth cell](./radio-icon-width)
- [RadioUncheck cell](./radio-uncheck)
- [Type appendix](/docs/appx/type)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
