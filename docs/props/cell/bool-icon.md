# BoolIcon ***(cell)***

<!-- synonyms: 체크박스 아이콘, 체크박스 이미지, 라디오 이미지, custom checkbox, bool icon cell -->

> `Type:"Bool"`인 셀에서 체크/체크해제 아이콘 모양을 변경합니다.  
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
|`0` | 기본 내장 체크박스 (`default`)|
|`1` | 내장 라디오 이미지|
|`2` | 무조건 middle 정렬되는 체크박스 (`0`보다 느림)|
|`3` | 무조건 middle 정렬되는 라디오 (`1`보다 느림)|
|`4` | `<input type="checkbox">` 객체 사용 (IE에서 빠름)|
|`5` | `<input type="radio">` 객체 사용 (IE에서 빠름)|
|`6` | `<div>` 객체로 체크박스 구현 (IE 호환성 보기에서 빠름)|

### Example
```javascript
// AR99 행의 CLS 셀에 HTML input 체크박스 적용
sheet.setAttribute(sheet.getRowById("AR99"), "CLS", "BoolIcon", 4);

// 사용자 이미지로 체크박스 표시
sheet.setAttribute(sheet.getRowById("AR99"), "CLS", "BoolIcon", "|Off.gif|On.gif");
```

### Read More
- [BoolIcon col](/docs/props/col/bool-icon)
- [BoolGroup cell](/docs/props/cell/bool-group)
- [Type appendix](/docs/appx/type)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
