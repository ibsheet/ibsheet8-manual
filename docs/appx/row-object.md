# 행 객체(Row Object)  ***(appendix)***
> sheet.[getFocusedRow](/docs/funcs/core/get-focused-row)()나 sheet.[getRowById](/docs/funcs/core/get-row-by-id)("AR11") 등의 함수를 통해 얻게 되는 데이터 행 객체는 해당 행의 값과, 각 열 별로 설정한 속성값([CanEdit](/docs/props/row/can-edit)나 [Visible](/docs/props/row/visible) 등) 그리고 주변행이나 부모행에 대한 링크 정보를 갖고 있습니다.

## Row의 값
행 객체가 갖고 있는 각 열의 값을 확인하거나 수정하실 수 있습니다.
```javascript
var row = sheet.getRowById("AR1");
var AmtColumnValue = row["AMT"]; //AMT 열의 값을 얻습니다.
row["AMT"] = 2300; //AR1행의 AMT 열의 값을 2300으로 수정합니다.
//수정된 값은 화면에 즉시 반영되지 않고, refreshCell() 이나 refreshRow()함수를 호출하셔야 반영됩니다.
```

## Row 객체에 직접 접근할 때 주의

[getValue](/docs/funcs/core/get-value) / [setValue](/docs/funcs/core/set-value)가 아니라 `row["col"]`로 값을 직접 읽거나 쓸 때는 아래를 주의합니다.

**1. 날짜(`Date`) 컬럼 — 내부에 타임스탬프로 저장**

row 객체의 날짜 값은 화면 표시 형태가 아니라 **타임스탬프**로 들어 있습니다. 화면에 보이는 형태로 꺼내려면 [getValue](/docs/funcs/core/get-value)나 전역 함수 [IBSheet.dateToString](/docs/static/date-to-string)을 사용합니다.
```javascript
sheet.getValue(row, "DateData");                    // "20240729"
row["DateData"];                                     // 1722240607605 (타임스탬프)
IBSheet.dateToString(row["DateData"], "yyyyMMdd");   // "20240729"
```
`setValue`를 쓰지 않고 날짜 값을 직접 넣을 때도 **타임스탬프**로 설정해야 합니다.

**2. `Text` 컬럼 — 데이터가 숫자면 숫자형으로 저장**

`Type:"Text"`로 만든 컬럼이라도 데이터가 숫자면 row 객체에는 **숫자(`number`)형**으로 저장됩니다. (`getValue`는 문자열로 반환)
```javascript
// 서버가 문자열 "123"으로 내려준 Text 컬럼
row["TextData"];                   // 123     (number — 숫자형으로 저장됨)
sheet.getValue(row, "TextData");   // "123"   (string)
```
[(col)OrigSearchData](/docs/props/col/orig-search-data)`:1`을 설정하면 변환 없이 **원본 타입 그대로** 둡니다(문자는 문자, 숫자는 숫자).  
타입에 흔들리지 않는 값이 필요하면 [getValue](/docs/funcs/core/get-value)나 [getString](/docs/funcs/core/get-string)을 사용하세요.

`Int` / `Float` 컬럼도 빈 값이 들어오면 `row["col"]` 직접 값이 `""` / `null` / `undefined`로 제각각이라, 바로 연산하면 `NaN`이 날 수 있습니다.  
숫자 연산 전에는 `Number(v) || 0` 같은 방어가 안전합니다. (빈 값 처리 상세: [(col)CanEmpty](/docs/props/col/can-empty))

**3. `Changed`(변경 상태)가 설정되지 않음**

[setValue](/docs/funcs/core/set-value)로 값을 바꾸면 행에 `Changed` 상태가 자동으로 표시되지만, **row 객체에 직접 대입하면 `Changed`가 설정되지 않습니다.** 변경 감지나 저장 시 데이터 추출이 되지 않으므로, 직접 대입이 불가피하면 `Changed`도 함께 설정해야 합니다.

## Row의 속성값
행 객체의 각 열에 부여한 속성을 확인 하거나 수정하실 수 있습니다.
```javascript
var row = sheet.getFocusedRow();
var isEditable = row["AMTCanEdit"]; //AMT 열의 수정가능여부를 확인합니다.
row["AMTCanEdit"] = 0; //포커스된 행의 AMT열의 수정가능여부를 수정불가로 변경합니다.
//속성값에 따라 refreshCell() 이나 refreshRow()함수를 호출하셔야 반영될 수 있습니다.
```

## Row의 링크정보
행객체는 각 행의 위의 행,아래 행, 부모행, 자식행에 대한 링크를 갖고 있습니다.

|Name|Description|
|---|---|
|nextSibling|아래 행 객체(트리 사용시에는 같은 부모 안에서 아래 형제 행. 없으면 null)|
|previousSibling|위 행 객체(트리 사용시에는 같은 부모 안에서 위 형제 행. 없으면 null)|
|firstChild|트리 사용시 현재 행 객체의 첫번째 자식행 객체|
|lastChild|트리 사용시 현재 행 객체의 마지막 자식행 객체|
|parentNode|부모행 객체|

```javascript
var row = sheet.getFocusedRow();
var nextRow = row.nextSibling; //포커스 된 행의 아래 행 객체
var parentRow = row.parentNode; //포커스 된 행의 부모행 객체
```

### Read More

- [행(Row) 구조에 대한 이해 getting started](/docs/start/row)
- [getFocusedRow method](/docs/funcs/core/get-focused-row)
- [getRowById method](/docs/funcs/core/get-row-by-id)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
