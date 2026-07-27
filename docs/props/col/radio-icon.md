# RadioIcon ***(col)***

<!-- synonyms: 라디오 아이콘, 라디오 이미지, custom radio, radio icon, 라디오 버튼 모양 -->

> `Type:"Radio"`인 열에서 라디오 아이콘 모양을 변경합니다.  
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
|`0` | 기본 내장 라디오 아이콘 / [Range](./range) 사용 시 내장 체크박스 아이콘 (`default`)|
|`1` | 내장 라디오 아이콘|
|`2` | 내장 체크박스 아이콘|
|`3` | `<input type="radio">` 객체 사용 / [Range](./range) 사용 시 `<input type="checkbox">` 객체|
|`4` | `<input type="radio">` 객체 사용|
|`5` | `<input type="checkbox">` 객체 사용|
|`6` | 아이콘 표시 안 함|

> `input` 객체를 사용하는 경우 그렇지 않은 옵션보다 성능이 느릴 수 있습니다.

### Example
```javascript
options.Cols = [
    // 라디오 컬럼에 체크박스 아이콘 사용
    {Type: "Radio", Name: "relation", RadioIcon: 2},

    // 사용자 이미지로 라디오 아이콘 설정
    {Type: "Radio", Name: "status", RadioIcon: "|OFF.gif|ON.gif"}
];
```

### Read More
- [RadioIcon cell](/docs/props/cell/radio-icon)
- [RadioIconWidth col](./radion-icon-width)
- [RadioUncheck col](./radio-uncheck)
- [Range col](./range)
- [HRadio col](./h-radio)
- [Type appendix](/docs/appx/type)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
