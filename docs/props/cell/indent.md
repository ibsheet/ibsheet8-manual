# Indent ***(cell)***

<!-- synonyms: Indent, 들여쓰기, 패딩, padding, 셀 padding, 셀 들여쓰기, 여백, 인덴트, 왼쪽 패딩, 오른쪽 패딩, 셀 여백 -->

> 문자열 정렬([Align](./align))에 따라 셀 좌측 또는 우측에 들여쓰기를 설정합니다.
>
> 숫자로 입력시 입력값*10px로 padding이 생성됩니다.
### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`number`|패딩 정도 (입력값 * 10px)|


### Example
```javascript
//특정 셀에 20px 정도 패딩을 생성
sheet.setAttribute(sheet.getRowById("AR99"), "CLS", "Indent", 2);
```

### Read More
- [Align cell](./align)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
