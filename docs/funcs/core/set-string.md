# setString ***(method)***
> 포맷이 적용된 문자열로 셀의 값을 설정합니다.  
> [setValue](/docs/funcs/core/set-value)가 원본값(코드값, 구분자 없는 값)을 직접 설정하는 것과 달리, `setString`은 화면에 표출되는 형태의 값으로 설정합니다.  
> 기본적으로 이 함수를 호출해도 편집 관련 이벤트(`onAfterChange`, `onEndEdit` 등)는 발생하지 않습니다.  
> 단, 데이터가 편집 상태일 때 `setString`을 호출하면 `onEndEdit` 이벤트가 발생합니다.  
> `Date` 타입: 구분자(`.` `/` `-`)가 포함된 날짜 문자열로 설정합니다. 구분자 종류는 관계없습니다. (예: `"2016/12/23"`, `"2016-12-23"`, `"2016.12.23"`)  
> `Enum, Radio` 타입: [EnumKeys](/docs/props/cell/enum-keys)가 정의된 경우 `EnumKeys`에 매핑된 코드값으로 저장됩니다.  

### Syntax
```javascript
void setString( row, col, val, render);
```

### Parameters

|Name|Type|Required| Description |
|----------|-----|---|----|
|row |`object`|<span class='required'>필수</span>|[데이터 로우 객체](/docs/appx/row-object)|
|col |`string`|<span class='required'>필수</span>|열이름|
|val |`string`|<span class='required'>필수</span>|입력값(셀 타입에 맞는 포맷 적용된 값) |
|render |`boolean`|<span class='optional'>선택</span>|즉시 화면 반영 여부<br/>`0(false)`:반영 안함<br/>`1(true)`:즉시 반영 (`default`)|

### setValue vs setString

| 컬럼 타입 | setValue | setString |
|---------|---------|---------|
| Date | 구분자 없는 날짜 (`"20161223"`) | 구분자 포함 날짜 (`.` `/` `-` 모두 허용, 예: `"2016/12/23"`) |
| Enum | 코드값 (`"01"`) | EnumKeys 매핑값 |
| 일반 Text | 저장값 그대로 | 저장값 그대로 (동일) |

### Return Value
***boolean*** : 값의 변경 여부 (값이 변경되면 `true`, 변경되지 않으면 `false`)

### Example
```javascript
var row = sheet.getRowById("AR5");

// Date 컬럼 - 포맷 적용 날짜 문자열로 설정
sheet.setString(row, "StartDate", "2016/12/23");  // 저장값: "20161223"

// setValue와 비교
sheet.setValue(row, "StartDate", "20161223");      // 동일한 결과
sheet.setString(row, "StartDate", "2016/12/23");   // 동일한 결과

// Enum 컬럼 - EnumKeys 매핑값으로 설정
// EnumKeys: "M;F", Enum: "남성;여성" 인 경우
sheet.setString(row, "Gender", "M");  // 화면표출: "남성"
```

### Read More

- [EnumKeys cell](/docs/props/cell/enum-keys)
- [getString method](./get-string)
- [getValue method](./get-value)
- [setValue method](./set-value)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.0.0.3|Enum 타입, Radio 타입의 Enum의 값을 EnumKeys와 매칭하는 기능 추가|
