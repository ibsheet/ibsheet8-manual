# RadioUncheck ***(col)***

<!-- synonyms: 라디오 체크해제, 라디오 선택 취소, 라디오 토글, radio uncheck, 같은 라디오 다시 클릭 -->

> `Type:"Radio"`인 열에서 이미 선택된 항목을 다시 클릭했을 때 체크해제를 허용할지 여부를 설정합니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)` | 체크해제 허용 안 함 (`default`)|
|`1(true)` | 체크해제 허용|

### Example
```javascript
options.Cols = [
    // 같은 라디오 항목 다시 클릭 시 체크해제 가능
    {Type: "Radio", Name: "relation", RadioUncheck: 1, ...}
];
```

### Read More
- [RadioUncheck cell](/docs/props/cell/radio-uncheck)
- [Uncheck col](./uncheck)
- [RadioIcon col](./radio-icon)
- [RadioIconWidth col](./radion-icon-width)
- [Range col](./range)
- [HRadio col](./h-radio)
- [Type appendix](/docs/appx/type)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
