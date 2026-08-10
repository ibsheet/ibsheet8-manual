# getCurrentStyle ***(method)***

<!-- synonyms: getCurrentStyle, get-current-style, 현재 스타일, 테마 조회, 시트 스타일, 배경색 조회, 글자색 조회, 스타일 정보, current, style, theme -->

> 현재 시트의 Def에 설정된 테마, 배경색, 글자색 및 Alternate 색상, 글자크기 정보를 문자열로 가져오는 메소드입니다.
>
> 테마를 제외한 속성의 default 값은 추가되지 않습니다.

### Syntax
```javascript
string getCurrentStyle();
```

### Return Value
***string 현재 시트의 Def에 설정된 배경색, 글자색 및 Alternate 색상, 글자크기 정보 값***

### Example
```javascript
// 현재 시트의 컬럼 정보를 담고 있는 문자열을 반환
sheet.getCurrentStyle();
```

### Read More
- [행(Row) 구조에 대한 이해 getting started](/docs/start/row)
- [setCurrentStyle method](./set-current-style)
- [AlternateColor row](/docs/props/row/alternate-color.md)
- [Color row](/docs/props/row/color.md)
- [TextColor row](/docs/props/row/text-color.md)
- [TextSize row](/docs/props/row/text-size.md)

### Since

|product|version|desc|
|---|---|---|
|core|8.3.0.18|기능 추가|
